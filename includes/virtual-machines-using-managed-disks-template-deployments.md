# <a name="using-managed-disks-in-azure-resource-manager-templates"></a><span data-ttu-id="939ee-101">Utilisation de disques gérés dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="939ee-101">Using Managed Disks in Azure Resource Manager Templates</span></span>

<span data-ttu-id="939ee-102">Ce document décrit les différences entre les disques gérés et les disques non gérés lorsque vous utilisez des modèles Azure Resource Manager pour configurer des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="939ee-102">This document walks through the differences between managed and unmanaged disks when using Azure Resource Manager templates to provision virtual machines.</span></span> <span data-ttu-id="939ee-103">Cela vous permettra de mettre à jour les modèles existants qui utilisent des disques non gérés en les remplaçant par des disques gérés.</span><span class="sxs-lookup"><span data-stu-id="939ee-103">This will help you to update existing templates that are using unmanaged Disks to managed disks.</span></span> <span data-ttu-id="939ee-104">Pour référence, nous utilisons le modèle [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) comme guide.</span><span class="sxs-lookup"><span data-stu-id="939ee-104">For reference, we are using the [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) template as a guide.</span></span> <span data-ttu-id="939ee-105">Vous pouvez consulter le modèle utilisant des [disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) et une version antérieure utilisant des [disques non gérés](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si vous voulez les comparer directement.</span><span class="sxs-lookup"><span data-stu-id="939ee-105">You can see the template using both [managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) and a prior version using [unmanaged disks](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) if you'd like to directly compare them.</span></span>

## <a name="unmanaged-disks-template-formatting"></a><span data-ttu-id="939ee-106">Mise en forme de modèle de disques non gérés</span><span class="sxs-lookup"><span data-stu-id="939ee-106">Unmanaged Disks template formatting</span></span>

<span data-ttu-id="939ee-107">Pour commencer, nous nous intéressons à la façon dont les disques non gérés sont déployés.</span><span class="sxs-lookup"><span data-stu-id="939ee-107">To begin, we take a look at how unmanaged disks are deployed.</span></span> <span data-ttu-id="939ee-108">Lorsque vous créez des disques non gérés, vous avez besoin d’un compte de stockage pour héberger les fichiers de disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="939ee-108">When creating unmanaged disks, you need a storage account to hold the VHD files.</span></span> <span data-ttu-id="939ee-109">Vous pouvez créer un compte de stockage ou en utiliser un existant.</span><span class="sxs-lookup"><span data-stu-id="939ee-109">You can create a new storage account or use one that already exists.</span></span> <span data-ttu-id="939ee-110">Cet article vous expliquera comment créer un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="939ee-110">This article will show you how to create a new storage account.</span></span> <span data-ttu-id="939ee-111">Pour ce faire, vous avez besoin d’une ressource de compte de stockage dans le bloc de ressources, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="939ee-111">To accomplish this, you need a storage account resource in the resources block as shown below.</span></span>

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

<span data-ttu-id="939ee-112">Dans l’objet de machine virtuelle, nous avons besoin d’une dépendance sur le compte de stockage pour nous assurer qu’il est créé avant la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="939ee-112">Within the virtual machine object, we need a dependency on the storage account to ensure that it's created before the virtual machine.</span></span> <span data-ttu-id="939ee-113">Dans la section `storageProfile`, nous spécifions ensuite l’URI complet de l’emplacement du disque dur virtuel, qui fait référence au compte de stockage et qui est nécessaire pour le disque de système d’exploitation et les disques de données.</span><span class="sxs-lookup"><span data-stu-id="939ee-113">Within the `storageProfile` section, we then specify the full URI of the VHD location, which references the storage account and is needed for the OS disk and any data disks.</span></span> 

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

## <a name="managed-disks-template-formatting"></a><span data-ttu-id="939ee-114">Mise en forme de modèle de disques gérés</span><span class="sxs-lookup"><span data-stu-id="939ee-114">Managed disks template formatting</span></span>

<span data-ttu-id="939ee-115">Avec Azure Managed Disks, le disque devient une ressource de niveau supérieur et ne requiert plus qu’un compte de stockage soit créé par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="939ee-115">With Azure Managed Disks, the disk becomes a top-level resource and no longer requires a storage account to be created by the user.</span></span> <span data-ttu-id="939ee-116">Les disques gérés ont d’abord été exposés dans la version de l’API `2016-04-30-preview`. Ils sont disponibles dans toutes les versions ultérieures de l’API et correspondent désormais au type de disque par défaut.</span><span class="sxs-lookup"><span data-stu-id="939ee-116">Managed disks were first exposed in the `2016-04-30-preview` API version, they are available in all subsequent API versions and are now the default disk type.</span></span> <span data-ttu-id="939ee-117">Les sections suivantes abordent les paramètres par défaut et décrivent en détail comment personnaliser davantage vos disques.</span><span class="sxs-lookup"><span data-stu-id="939ee-117">The following sections walk through the default settings and detail how to further customize your disks.</span></span>

> [!NOTE]
> <span data-ttu-id="939ee-118">Il est recommandé d’utiliser une version d’API plus récente que `2016-04-30-preview` en raison de modifications intervenues entre les versions `2016-04-30-preview` et `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="939ee-118">It is recommended to use an API version later than `2016-04-30-preview` as there were breaking changes between `2016-04-30-preview` and `2017-03-30`.</span></span>
>
>

### <a name="default-managed-disk-settings"></a><span data-ttu-id="939ee-119">Paramètres de disque géré par défaut</span><span class="sxs-lookup"><span data-stu-id="939ee-119">Default managed disk settings</span></span>

<span data-ttu-id="939ee-120">Pour créer une machine virtuelle avec des disques gérés, vous n’avez plus besoin créer la ressource de compte de stockage et vous pouvez mettre à jour votre ressource de machine virtuelle comme suit.</span><span class="sxs-lookup"><span data-stu-id="939ee-120">To create a VM with managed disks, you no longer need to create the storage account resource and can update your virtual machine resource as follows.</span></span> <span data-ttu-id="939ee-121">Notez en particulier que `apiVersion` reflète `2017-03-30`, et que `osDisk` et `dataDisks` ne font plus référence à un URI spécifique pour le disque dur virtuel.</span><span class="sxs-lookup"><span data-stu-id="939ee-121">Specifically note that the `apiVersion` reflects `2017-03-30` and the `osDisk` and `dataDisks` no longer refer to a specific URI for the VHD.</span></span> <span data-ttu-id="939ee-122">Lors du déploiement sans spécification de propriétés supplémentaires, le disque utilisera le [stockage LRS standard](../articles/storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="939ee-122">When deploying without specifying additional properties, the disk will use [Standard LRS storage](../articles/storage/common/storage-redundancy.md).</span></span> <span data-ttu-id="939ee-123">Si aucun nom n’est spécifié, il prend le format `<VMName>_OsDisk_1_<randomstring>` pour le disque de système d’exploitation et `<VMName>_disk<#>_<randomstring>` pour chaque disque de données.</span><span class="sxs-lookup"><span data-stu-id="939ee-123">If no name is specified, it takes the format of `<VMName>_OsDisk_1_<randomstring>` for the OS disk and `<VMName>_disk<#>_<randomstring>` for each data disk.</span></span> <span data-ttu-id="939ee-124">Par défaut, le chiffrement de disque Azure est désactivé ; la mise en cache est Lecture/Écriture pour le disque de système d’exploitation et Aucune pour les disques de données.</span><span class="sxs-lookup"><span data-stu-id="939ee-124">By default, Azure disk encryption is disabled; caching is Read/Write for the OS disk and None for data disks.</span></span> <span data-ttu-id="939ee-125">Vous avez pu remarquer dans l’exemple ci-dessous qu’il existe toujours une dépendance de compte de stockage, bien que cela concerne uniquement le stockage de diagnostics et n’est pas nécessaire pour le stockage de disques.</span><span class="sxs-lookup"><span data-stu-id="939ee-125">You may notice in the example below there is still a storage account dependency, though this is only for storage of diagnostics and is not needed for disk storage.</span></span>

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

### <a name="using-a-top-level-managed-disk-resource"></a><span data-ttu-id="939ee-126">Utilisation d’une ressource de disque géré de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="939ee-126">Using a top-level managed disk resource</span></span>

<span data-ttu-id="939ee-127">Au lieu de spécifier la configuration du disque dans l’objet de machine virtuelle, vous pouvez créer une ressource de disque de niveau supérieur et l’attacher dans le cadre de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="939ee-127">As an alternative to specifying the disk configuration in the virtual machine object, you can create a top-level disk resource and attach it as part of the virtual machine creation.</span></span> <span data-ttu-id="939ee-128">Par exemple, nous pouvons créer une ressource de disque comme suit pour l’utiliser comme un disque de données.</span><span class="sxs-lookup"><span data-stu-id="939ee-128">For example, we can create a disk resource as follows to use as a data disk.</span></span>

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

<span data-ttu-id="939ee-129">Dans l’objet de machine virtuelle, nous pouvons ensuite faire référence à cet objet de disque devant être attaché.</span><span class="sxs-lookup"><span data-stu-id="939ee-129">Within the VM object, we can then reference this disk object to be attached.</span></span> <span data-ttu-id="939ee-130">Spécifier l’ID de ressource du disque géré que nous avons créé dans la propriété `managedDisk` permet d’attacher le disque lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="939ee-130">Specifying the resource ID of the managed disk we created in the `managedDisk` property allows the attachment of the disk as the VM is created.</span></span> <span data-ttu-id="939ee-131">Vous pouvez constater que la propriété `apiVersion` de la ressource de la machine virtuelle est définie sur `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="939ee-131">Note that the `apiVersion` for the VM resource is set to `2017-03-30`.</span></span> <span data-ttu-id="939ee-132">Notez également que nous avons créé une dépendance sur la ressource de disque pour nous assurer qu’elle est correctement créée avant la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="939ee-132">Also note that we've created a dependency on the disk resource to ensure it's successfully created before VM creation.</span></span> 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a><span data-ttu-id="939ee-133">Créer des groupes à haute disponibilité gérés avec des machines virtuelles à l’aide de disques gérés</span><span class="sxs-lookup"><span data-stu-id="939ee-133">Create managed availability sets with VMs using managed disks</span></span>

<span data-ttu-id="939ee-134">Pour créer des groupes à haute disponibilité gérés avec des machines virtuelles à l’aide de disques gérés, ajoutez l’objet `sku` à la ressource de groupe à haute disponibilité et définissez la propriété `name` sur `Aligned`.</span><span class="sxs-lookup"><span data-stu-id="939ee-134">To create managed availability sets with VMs using managed disks, add the `sku` object to the availability set resource and set the `name` property to `Aligned`.</span></span> <span data-ttu-id="939ee-135">Cela garantit que les disques de chaque machine virtuelle sont suffisamment isolés les uns des autres pour éviter les points uniques de défaillance.</span><span class="sxs-lookup"><span data-stu-id="939ee-135">This ensures that the disks for each VM are sufficiently isolated from each other to avoid single points of failure.</span></span> <span data-ttu-id="939ee-136">Vous pouvez aussi remarquer que la propriété `apiVersion` de la ressource de groupe à haute disponibilité est définie sur `2017-03-30`.</span><span class="sxs-lookup"><span data-stu-id="939ee-136">Also note that the `apiVersion` for the availability set resource is set to `2017-03-30`.</span></span>

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

### <a name="additional-scenarios-and-customizations"></a><span data-ttu-id="939ee-137">Personnalisations et scénarios supplémentaires</span><span class="sxs-lookup"><span data-stu-id="939ee-137">Additional scenarios and customizations</span></span>

<span data-ttu-id="939ee-138">Pour obtenir des informations complètes sur les spécifications de l’API REST, veuillez consulter la [documentation de l’API REST portant sur la création d’un disque géré](/rest/api/manageddisks/disks/disks-create-or-update).</span><span class="sxs-lookup"><span data-stu-id="939ee-138">To find full information on the REST API specifications, please review the [create a managed disk REST API documentation](/rest/api/manageddisks/disks/disks-create-or-update).</span></span> <span data-ttu-id="939ee-139">Vous trouverez d’autres scénarios, ainsi que des valeurs par défaut et acceptables qui peuvent être envoyées à l’API via des déploiements de modèle.</span><span class="sxs-lookup"><span data-stu-id="939ee-139">You will find additional scenarios, as well as default and acceptable values that can be submitted to the API through template deployments.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="939ee-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="939ee-140">Next steps</span></span>

* <span data-ttu-id="939ee-141">Pour des modèles complets qui utilisent des disques gérés, consultez les liens suivants du référentiel de démarrage rapide Azure.</span><span class="sxs-lookup"><span data-stu-id="939ee-141">For full templates that use managed disks visit the following Azure Quickstart Repo links.</span></span>
    * [<span data-ttu-id="939ee-142">Machine virtuelle Windows avec disques gérés</span><span class="sxs-lookup"><span data-stu-id="939ee-142">Windows VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [<span data-ttu-id="939ee-143">Machine virtuelle Linux avec disques gérés</span><span class="sxs-lookup"><span data-stu-id="939ee-143">Linux VM with managed disk</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [<span data-ttu-id="939ee-144">Liste complète des modèles de disque géré</span><span class="sxs-lookup"><span data-stu-id="939ee-144">Full list of managed disk templates</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="939ee-145">Consultez le document [Vue d’ensemble d’Azure Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md) pour en savoir plus sur les disques gérés.</span><span class="sxs-lookup"><span data-stu-id="939ee-145">Visit the [Azure Managed Disks Overview](../articles/virtual-machines/windows/managed-disks-overview.md) document to learn more about managed disks.</span></span>
* <span data-ttu-id="939ee-146">Passez en revue la documentation de référence sur les modèles pour les ressources de machine virtuelle en consultant le document [de référence sur le modèle Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines).</span><span class="sxs-lookup"><span data-stu-id="939ee-146">Review the template reference documentation for virtual machine resources by visiting the [Microsoft.Compute/virtualMachines template reference](/templates/microsoft.compute/virtualmachines) document.</span></span>
* <span data-ttu-id="939ee-147">Passez en revue la documentation de référence sur les modèles pour les ressources de disque en consultant le document [de référence sur le modèle Microsoft.Compute/disks](/templates/microsoft.compute/disks).</span><span class="sxs-lookup"><span data-stu-id="939ee-147">Review the template reference documentation for disk resources by visiting the [Microsoft.Compute/disks template reference](/templates/microsoft.compute/disks) document.</span></span>
 
