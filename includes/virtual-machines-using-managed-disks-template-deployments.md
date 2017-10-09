# <a name="using-managed-disks-in-azure-resource-manager-templates"></a>Utilisation de disques gérés dans les modèles Azure Resource Manager

Ce document décrit les différences de hello entre disques managées et non managées, avec des machines virtuelles du tooprovision de modèles Azure Resource Manager. Cela vous permet de tooupdate les modèles existants qui utilisent des disques toomanaged disques non managés. Pour référence, nous utilisons hello [101-vm-simple-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows) modèle comme guide. Vous pouvez voir le modèle hello à l’aide de deux [des disques gérés par](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows/azuredeploy.json) une version antérieure à l’aide de [non managée disques](https://github.com/Azure/azure-quickstart-templates/tree/93b5f72a9857ea9ea43e87d2373bf1b4f724c6aa/101-vm-simple-windows/azuredeploy.json) si vous souhaitez que toodirectly les comparer.

## <a name="unmanaged-disks-template-formatting"></a>Mise en forme de modèle de disques non gérés

toobegin, nous nous intéressons à des disques comment non managées sont déployés. Lorsque vous créez des disques non managés, vous avez besoin d’un fichier de disque dur virtuel de stockage compte toohold hello. Vous pouvez créer un compte de stockage ou en utiliser un existant. Cet article vous indiquent comment toocreate un compte de stockage. tooaccomplish, vous avez besoin d’une ressource de compte de stockage dans le bloc de ressources hello comme indiqué ci-dessous.

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

Au sein de l’objet ordinateur virtuel de hello, nous avons besoin d’une dépendance sur tooensure de compte de stockage hello qu’il a créé avant que hello virtual machine. Au sein de hello `storageProfile` section, nous spécifions puis hello URI complet de hello emplacement de disque dur virtuel, ce qui fait référence à compte de stockage hello et est nécessaire pour les disques de hello du système d’exploitation et les disques de données. 

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

## <a name="managed-disks-template-formatting"></a>Mise en forme de modèle de disques gérés

Avec des disques Azure géré, disque de hello devient une ressource de niveau supérieur et ne requiert plus un toobe de compte de stockage créé par l’utilisateur de hello. Disques gérés ont été exposées tout d’abord Bonjour `2016-04-30-preview` version de l’API, ils sont disponibles dans toutes les versions ultérieures de API et sont désormais de type de disque par défaut hello. Bonjour sections suivantes parcourir les paramètres par défaut de hello et décrit en détail comment toofurther personnaliser vos disques.

> [!NOTE]
> Il est recommandé de toouse une API version postérieure à `2016-04-30-preview` en raison de modifications avec rupture entre `2016-04-30-preview` et `2017-03-30`.
>
>

### <a name="default-managed-disk-settings"></a>Paramètres de disque géré par défaut

toocreate une machine virtuelle avec des disques gérés, vous n’avez plus besoin de ressources de compte de stockage de hello toocreate et peut mettre à jour votre ressource de machine virtuelle comme suit. Notez en particulier les que hello `apiVersion` reflète `2017-03-30` et hello `osDisk` et `dataDisks` ne sont plus faire référence tooa URI spécifique pour hello disque dur virtuel. Lors du déploiement sans spécifier de propriétés supplémentaires, disque de hello utilisera [les stockage LRS Standard](../articles/storage/common/storage-redundancy.md). Si aucun nom n’est spécifié, il prend format hello `<VMName>_OsDisk_1_<randomstring>` pour le disque de hello du système d’exploitation et `<VMName>_disk<#>_<randomstring>` pour chaque disque de données. Par défaut, le chiffrement de disque Azure est désactivé ; la mise en cache d’est en lecture/écriture pour les disques de hello du système d’exploitation et None pour les disques de données. Vous pouvez le remarquer dans l’exemple hello ci-dessous qu'est toujours une dépendance de compte de stockage, bien que cela est uniquement pour le stockage de diagnostics et n’est pas nécessaire pour le stockage sur disque.

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

### <a name="using-a-top-level-managed-disk-resource"></a>Utilisation d’une ressource de disque géré de niveau supérieur

Comme une configuration de disque toospecifying autre hello dans l’objet d’ordinateur virtuel hello, vous pouvez créer une ressource de disque de niveau supérieur et attacher en tant que partie de la création de machine virtuelle hello. Par exemple, nous pouvons créer une ressource de disque comme suit toouse comme disque de données.

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

Au sein de l’objet d’ordinateur virtuel hello, nous pouvons ensuite référencer cette toobe d’objet de disque attaché. Spécifier l’ID de ressource hello Hello gérés disque que nous avons créé dans hello `managedDisk` propriété permet de hello pièce jointe du disque de hello hello machine virtuelle est créée. Notez que hello `apiVersion` pour hello ressource d’ordinateur virtuel est défini trop`2017-03-30`. Notez également que nous avons créé une dépendance sur tooensure de ressource de disque hello qu'il est créé avec succès avant la création d’ordinateurs virtuels. 

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

### <a name="create-managed-availability-sets-with-vms-using-managed-disks"></a>Créer des groupes à haute disponibilité gérés avec des machines virtuelles à l’aide de disques gérés

toocreate gérés disponibilité jeux avec des machines virtuelles à l’aide de disques gérés, ajoutez hello `sku` disponibilité toohello de l’objet défini des ressources et hello `name` propriété trop`Aligned`. Cela garantit que les disques hello pour chaque machine virtuelle sont suffisamment isolées les uns des autres tooavoid points de défaillance uniques. Notez également que hello `apiVersion` pour la ressource à haute disponibilité de hello est défini trop`2017-03-30`.

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

### <a name="additional-scenarios-and-customizations"></a>Personnalisations et scénarios supplémentaires

toofind des informations complètes sur les spécifications des API REST hello, passez en revue hello [créer un documentation de l’API REST de disque géré](/rest/api/manageddisks/disks/disks-create-or-update). Vous trouverez d’autres scénarios, ainsi que par défaut et les valeurs acceptables qui peuvent être des API toohello soumis par le biais des déploiements de modèle. 

## <a name="next-steps"></a>Étapes suivantes

* Pour les modèles complètes qui utilisent des disques gérés visitez hello suivant les liens de dépôt de démarrage rapide d’Azure.
    * [Machine virtuelle Windows avec disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-windows)
    * [Machine virtuelle Linux avec disques gérés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-simple-linux)
    * [Liste complète des modèles de disque géré](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* Visitez hello [vue d’ensemble des disques Azure administrés](../articles/virtual-machines/windows/managed-disks-overview.md) toolearn document savoir plus sur des disques gérés.
* Passez en revue la documentation de référence de modèle hello pour les ressources de l’ordinateur virtuel en visitant hello [référence de modèle Microsoft.Compute/virtualMachines](/templates/microsoft.compute/virtualmachines) document.
* Passez en revue la documentation de référence de modèle hello pour les ressources de disque en visitant hello [référence de modèle Microsoft.Compute/disks](/templates/microsoft.compute/disks) document.
 
