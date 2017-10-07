---
title: "ordinateurs aaaVirtual dans un modèle Azure Resource Manager | Microsoft Azure"
description: "En savoir plus sur la ressource d’ordinateur virtuel hello est défini dans un modèle Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a>Machines virtuelles dans un modèle Azure Resource Manager

Cet article décrit les aspects d’un modèle Azure Resource Manager s’applique toovirtual machines. Cet article ne décrit pas un modèle complet pour la création d’une machine virtuelle ; pour cela, vous avez besoin de définitions de ressource pour des comptes de stockage, d'interfaces réseau, d'adresses IP publiques et de réseaux virtuels. Pour plus d’informations sur la façon dont ces ressources peuvent être définis, consultez hello [procédure pas à pas de gestionnaire de ressources du modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Il existe de nombreux [modèles dans la galerie de hello](https://azure.microsoft.com/documentation/templates/?term=VM) qui incluent des ressources de machine virtuelle hello. Les éléments qui peuvent être inclus dans un modèle ne sont tous décrits ici.

Cet exemple montre une section de ressources standard d’un modèle pour la création d’un nombre spécifié de machines virtuelles :

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
>Cet exemple repose sur un compte de stockage créé précédemment. Vous pouvez créer le compte de stockage hello en la déployant à partir du modèle de hello. exemple de Hello s’appuie également sur une interface réseau et ses ressources dépendantes qui sont définies dans le modèle de hello. Ces ressources ne sont pas affichés dans l’exemple de hello.
>
>

## <a name="api-version"></a>Version de l'API

Lorsque vous déployez des ressources à l’aide d’un modèle, vous avez toospecify une version de hello API toouse. Hello montre une ressource d’ordinateur virtuel hello à l’aide de cet élément apiVersion :

```
"apiVersion": "2016-04-30-preview",
```

version de Hello de hello API que vous spécifiez dans votre modèle affecte les propriétés que vous pouvez définir dans le modèle de hello. En règle générale, vous devez sélectionner la version plus récente de l’API hello lors de la création de modèles. Pour les modèles existants, vous pouvez décider si vous souhaitez toocontinue à l’aide d’une version antérieure de l’API ou mettre à jour votre modèle pour hello dernière version tootake un avantage des nouvelles fonctionnalités.

Utilisez ces possibilités d’obtention de versions plus récentes de l’API hello :

- API REST - [Répertorier tous les fournisseurs de ressources](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)
- PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)
- Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)

## <a name="parameters-and-variables"></a>Paramètres et variables

[Paramètres](../../resource-group-authoring-templates.md) facilitent vous toospecify des valeurs pour le modèle de hello lorsque vous l’exécutez. Cette section de paramètres est utilisée dans l’exemple de hello :

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

Lorsque vous déployez le modèle d’exemple hello, vous entrez des valeurs pour le nom de hello et le mot de passe du compte d’administrateur hello sur chaque machine virtuelle et hello le numéro de toocreate de machines virtuelles. Vous pouvez hello spécifiant des valeurs de paramètre dans un fichier distinct qui est géré par le modèle de hello, ou en fournissant des valeurs lorsque vous y êtes invité.

[Variables](../../resource-group-authoring-templates.md) simplifient vous tooset des valeurs dans un modèle hello qui sont utilisés à plusieurs reprises tout au long ou qui peut changer au fil du temps. Cette section de variables est utilisée dans l’exemple de hello :

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

Lorsque vous déployez le modèle d’exemple hello, valeurs des variables sont utilisées pour le nom de hello et l’identificateur de compte de stockage hello créé précédemment. Variables sont également des paramètres de hello tooprovide utilisé pour l’extension de diagnostic hello. Hello d’utilisation [meilleures pratiques pour la création de modèles Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp vous décidez comment toostructure hello paramètres et les variables dans votre modèle.

## <a name="resource-loops"></a>boucles de ressources

Lorsque vous avez besoin de plusieurs machines virtuelles pour votre application, vous pouvez utiliser un élément copy dans un modèle. Cet élément facultatif effectue une itération sur la création de nombre de hello d’ordinateurs virtuels que vous avez spécifié en tant que paramètre :

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

En outre, notez dans l’exemple hello hello index de boucle est utilisé lorsque certaines hello spécifiant des valeurs pour la ressource de hello. Par exemple, si vous avez entré un nombre d’instances de trois, noms hello de disques de système d’exploitation hello sont myOSDisk1, myOSDisk2 et myOSDisk3 :

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
>Cet exemple utilise des disques gérés pour les ordinateurs virtuels de hello.
>
>

Gardez à l’esprit nécessitant la création d’une boucle pour une ressource dans le modèle de hello vous toouse hello boucle lors de la création ou de l’accès à d’autres ressources. Par exemple, plusieurs machines virtuelles ne peut pas utiliser hello même interface réseau, donc si votre modèle effectue une itération sur la création de trois machines virtuelles, il doit également faire une boucle dans la création de trois interfaces réseau. Lorsque vous affectez un tooa d’interface réseau virtuelle, les index de boucle hello est tooidentify utilisé il :

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a>Dépendances

La plupart des ressources en dépendent autres toowork ressources correctement. Machines virtuelles doit être associés à un réseau virtuel et un toodo qu’il nécessite une interface réseau. Hello [dependsOn](../../resource-group-define-dependencies.md) élément est utilisé toomake que cette interface de réseau hello est prêt toobe utilisé avant la création des machines virtuelles de hello :

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

Resource Manager déploie en parallèle les ressources qui ne dépendent pas d'une autre ressource en cours de déploiement. Soyez prudent lors de la définition des dépendances car vous pouvez accidentellement ralentir votre déploiement en spécifiant des dépendances inutiles. Les dépendances peuvent couvrir plusieurs ressources. Par exemple, interface de réseau hello dépend adresse IP publique de hello et ressources du réseau virtuel.

Comment savoir si une dépendance est nécessaire ? Examinez les valeurs hello que vous définissez dans le modèle de hello. Si un élément dans la définition de ressource d’ordinateur virtuel hello pointe tooanother ressource déployée dans hello même modèle, vous avez besoin d’une dépendance. Par exemple, votre exemple de machine virtuelle définit un profil de réseau :

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

tooset cette propriété, l’interface de réseau hello doit exister. Vous avez donc besoin d’une dépendance. Vous devez également tooset une dépendance lorsqu’une ressource (enfant) est définie dans une autre ressource (parent). Par exemple, les paramètres de diagnostic hello et extensions de script personnalisé sont définies en tant que ressources enfants de l’ordinateur virtuel de hello. Ils ne peuvent pas être créés jusqu'à ce que l’ordinateur virtuel de hello existe. Par conséquent, les deux ressources sont marqués comme dépendant de la machine virtuelle de hello.

## <a name="profiles"></a>Profils

Plusieurs éléments de profil sont utilisés lors de la définition d’une ressource de machine virtuelle. Certains sont obligatoires, et d’autres facultatifs. Par exemple, les éléments hardwareProfile, osProfile, storageProfile et VM hello sont obligatoires, mais hello diagnosticsProfile est facultatif. Ces profils définissent des paramètres tels que :
   
- [taille](sizes.md)
- [nom](/architecture/best-practices/naming-conventions) et informations d’identification
- disque et [paramètres du système d’exploitation](cli-ps-findimage.md)
- [interface réseau](../../virtual-network/virtual-networks-multiple-nics.md) 
- diagnostics de démarrage

## <a name="disks-and-images"></a>Disques et images
   
Dans Azure, les fichiers de disque dur virtuel peuvent représenter [des disques ou des images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Lorsque le système d’exploitation de hello dans un fichier de disque dur virtuel est spécialisé toobe un ordinateur virtuel spécifique, il est référencé tooas un disque. Lorsque le système d’exploitation de hello dans un fichier de disque dur virtuel est généralisée toobe utilisé toocreate de machines virtuelles, il est référencé tooas une image.   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a>Créer des machines virtuelles et des disques à partir d’une image de plateforme

Lorsque vous créez une machine virtuelle, vous devez décider quels toouse du système d’exploitation. élément d’imageReference Hello est système de d’exploitation hello toodefine utilisé d’une machine virtuelle. Hello montre une définition pour un système d’exploitation Windows :

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

Si vous souhaitez toocreate à un système d’exploitation Linux, vous pouvez utiliser cette définition :

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

Paramètres de configuration de disque de système d’exploitation hello assignés avec un élément d’osDisk hello. Hello exemple définit un nouveau disque géré par hello jeu en mode de mise en cache trop**ReadWrite** et qu’un disque hello est créé à partir d’un [image de plateforme](cli-ps-findimage.md):

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a>Créer de nouvelles machines virtuelles à partir de disques gérés existants

Si vous souhaitez que les ordinateurs virtuels de toocreate à partir de disques existants, supprimez hello imageReference et éléments d’osProfile hello et définir ces paramètres de disque :

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a>Créer de nouvelles machines virtuelles à partir d'une image gérée

Si vous voulez toocreate un ordinateur virtuel à partir d’une image managée, modifier l’élément imageReference hello et définir ces paramètres de disque :

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a>Connecter des disques de données

Vous pouvez éventuellement ajouter des disques de données toohello machines virtuelles. Hello [nombre de disques](sizes.md) dépend de taille hello du disque de système d’exploitation que vous utilisez. Avec hello taille des machines virtuelles de hello défini tooStandard_DS1_v2, nombre maximal de hello de disques de données qui pourraient être ajoutées toohello les est deux. Dans l’exemple de hello, un disque de données managé est ajouté tooeach machine virtuelle :

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a>Extensions

Bien que [extensions](extensions-features.md) sont une ressource distincte, ils sont étroitement liés tooVMs. Extensions peuvent être ajoutées en tant qu’une ressource enfant de hello machine virtuelle ou comme une ressource distincte. Il montre Hello hello [Extension Diagnostics](extensions-diagnostics-template.md) ajouté toohello VM :

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

Cette ressource d’extension utilise la variable de storageName hello et les valeurs de tooprovide de variables de diagnostic hello. Si vous souhaitez que les données de salutation toochange collectées par cette extension, vous pouvez ajouter plus variable wadperfcounters de performances des compteurs toohello. Vous pouvez également choisir les données de diagnostic tooput hello dans un autre compte de stockage que le stockage des disques de machine virtuelle hello.

Il existe de nombreuses extensions que vous pouvez installer sur un ordinateur virtuel, mais hello plus utile est probablement hello [Extension de Script personnalisé](extensions-customscript.md). Dans l’exemple de hello, un script PowerShell nommé start.ps1 s’exécute sur chaque ordinateur virtuel lors du premier démarrage :

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

script de start.ps1 Hello permettre effectuer de nombreuses tâches de configuration. Par exemple, les disques de données hello ajoutés dans l’exemple de hello toohello machines virtuelles ne sont pas initialisés ; Vous pouvez utiliser un script personnalisé de tooinitialize les. Si vous avez plusieurs toodo de tâches de démarrage, vous pouvez utiliser des autres scripts PowerShell hello start.ps1 fichier toocall dans le stockage Azure. exemple de Hello utilise PowerShell, mais vous pouvez utiliser toute méthode de script qui est disponible sur le système d’exploitation hello que vous utilisez.

Vous pouvez voir l’état hello d’extensions hello installé à partir des paramètres d’Extensions hello dans le portail de hello :

![Obtenir l’état de l’extension](./media/template-description/virtual-machines-show-extensions.png)

Vous pouvez également obtenir des informations sur l’extension à l’aide de hello **Get-AzureRmVMExtension** PowerShell commande hello **get d’extension de machine virtuelle** commande Azure CLI 2.0 ou hello **obtenir des informations d’extension**  API REST.

## <a name="deployments"></a>Déploiements

Lorsque vous déployez un modèle, les ressources de hello pistes Azure que vous avez déployé en tant que groupe et automatiquement assigne un nom de groupe toothis déployé. nom de Hello du déploiement de hello est hello identique au nom du modèle de hello hello.

Si vous êtes obtenir des informations sur l’état de hello des ressources de déploiement de hello, vous pouvez utiliser le panneau de groupe de ressources hello Bonjour portail Azure :

![Obtenir les informations de déploiement](./media/template-description/virtual-machines-deployment-info.png)
    
Il n’est pas un problème toouse hello des mêmes ressources toocreate de modèle ou tooupdate des ressources existantes. Lorsque vous utilisez des modèles de toodeploy de commandes, vous avez hello opportunité toosay qui [mode](../../resource-group-template-deploy.md) vous souhaitez toouse. Hello peut être défini tooeither **Complete** ou **incrémentiel**. valeur par défaut Hello est toodo les mises à jour incrémentielles. Soyez prudent lorsque vous utilisez hello **Complete** mode, car vous pouvez supprimer accidentellement des ressources. Lorsque vous définissez le mode hello trop**Complete**, Gestionnaire de ressources supprime toutes les ressources dans le groupe de ressources hello qui ne sont pas dans le modèle de hello.

## <a name="next-steps"></a>Étapes suivantes

- Créez votre propre modèle à l’aide de la rubrique [Création de modèles Azure Resource Manager](../../resource-group-authoring-templates.md).
- Déployer le modèle hello que vous avez créé à l’aide de [créer une machine virtuelle Windows avec un modèle de gestionnaire de ressources](ps-template.md).
- Découvrez comment toomanage hello machines virtuelles que vous avez créée en examinant [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
