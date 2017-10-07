---
title: aaaOMS extension de machine virtuelle Azure pour Windows | Documents Microsoft
description: "Déployer l’agent OMS de hello sur la machine virtuelle de Windows à l’aide d’une extension de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: feae6176-2373-4034-b5d9-a32c6b4e1f10
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: nepeters
ms.openlocfilehash: 3000f66c0acdec1d1fad2125b8c6b72a92b1ec92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-windows"></a>Extension de machine virtuelle OMS pour Windows

Operations Management Suite (OMS) fournit des fonctionnalités de surveillance, d’alerte et de correction des alertes sur le ressources cloud et locales. Hello, extension de machine virtuelle de l’Agent OMS pour Windows est publié et pris en charge par Microsoft. extension de Hello installe l’agent OMS de hello sur des machines virtuelles et inscrit les machines virtuelles dans un espace de travail OMS existant. Cette hello de détails de document pris en charge plates-formes, les configurations et les options de déploiement pour hello extension de machine virtuelle OMS pour Windows.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation
Hello extension OMS Agent pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.

### <a name="internet-connectivity"></a>Connectivité Internet
Hello extension OMS Agent pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet. 

## <a name="extension-schema"></a>Schéma d’extensions

Hello JSON suivant montre schéma hello pour hello extension OMS Agent. extension de Hello requiert hello espace de travail et Id de clé à partir de l’espace de travail OMS hello cible, elles sont accessibles dans portail OMS : hello. Étant donné que la clé d’espace de travail hello doit être traité comme des données sensibles, il doit être stocké dans une configuration protégée. Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello. Notez que **workspaceId** et **workspaceKey** respectent la casse.

```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```
### <a name="property-values"></a>Valeurs de propriétés

| Nom | Valeur/Exemple |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | MicrosoftMonitoringAgent |
| typeHandlerVersion | 1.0 |
| workspaceId (par exemple) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (par exemple) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |

## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension OMS Agent pendant un déploiement de modèle Azure Resource Manager. Vous trouverez un exemple de modèle qui inclut l’extension de machine virtuelle de l’Agent OMS hello sur hello [galerie de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-windows-vm). 

Hello JSON pour une extension de machine virtuelle peut être imbriquée dans une ressource d’ordinateur virtuel hello ou placé au niveau racine de hello ou un niveau supérieur d’un modèle de gestionnaire de ressources JSON. la sélection élective Hello Hello JSON affecte la valeur hello du nom de la ressource hello et type. Pour plus d’informations, consultez [Définition du nom et du type des ressources enfants](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hello suppose extension d’OMS hello est imbriquée dans la ressource d’ordinateur virtuel hello. Lors de l’imbrication des ressources d’extension de hello, hello JSON est placée dans hello `"resources": []` objet de machine virtuelle de hello.


```json
{
    "type": "extensions",
    "name": "OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

Lorsque vous placez l’extension hello JSON au niveau racine hello du modèle de hello, nom de la ressource hello inclut un ordinateur virtuel de référence toohello parent, et type de hello reflète configuration imbriqués de hello. 

```json
{
    "type": "Microsoft.Compute/virtualMachines/extensions",
    "name": "<parentVmResource>/OMSExtension",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.EnterpriseCloud.Monitoring",
        "type": "MicrosoftMonitoringAgent",
        "typeHandlerVersion": "1.0",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "workspaceId": "myWorkSpaceId"
        },
        "protectedSettings": {
            "workspaceKey": "myWorkspaceKey"
        }
    }
}
```

## <a name="powershell-deployment"></a>Déploiement PowerShell

Hello `Set-AzureRmVMExtension` commande peut être utilisé toodeploy hello Agent OMS machine virtuelle extension tooan machine virtuelle existante. Avant d’exécuter la commande hello, les configurations publiques et privées hello doivent toobe stockée dans une table de hachage de PowerShell. 

```powershell
$PublicSettings = @{"workspaceId" = "myWorkspaceId"}
$ProtectedSettings = @{"workspaceKey" = "myWorkspaceKey"}

Set-AzureRmVMExtension -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
    -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" `
    -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
    -ExtensionType "MicrosoftMonitoringAgent" `
    -TypeHandlerVersion 1.0 `
    -Settings $PublicSettings `
    -ProtectedSettings $ProtectedSettings `
    -Location WestUS ` 
```

## <a name="troubleshoot-and-support"></a>Dépannage et support technique

### <a name="troubleshoot"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello. état du déploiement hello toosee des extensions pour un ordinateur virtuel donné, hello exécution suite à l’aide de la commande hello module PowerShell Azure.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\
```

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
