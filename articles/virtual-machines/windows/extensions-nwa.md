---
title: "aaaAzure extension de machine virtuelle de l’Agent de l’Observateur réseau pour Windows | Documents Microsoft"
description: "Déployer hello Agent de l’Observateur réseau sur l’ordinateur virtuel de Windows à l’aide d’une extension de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a>Extension de machine virtuelle Agent Network Watcher pour Windows

## <a name="overview"></a>Vue d'ensemble

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) est un service d’analyse, de diagnostic et d’analytique des performances réseau permettant de surveiller les réseaux Azure. Hello, extension de machine virtuelle de l’Agent de l’Observateur réseau est obligatoire pour certaines des fonctionnalités de l’Observateur réseau hello sur des machines virtuelles. notamment la capture du trafic réseau à la demande et d’autres fonctionnalités avancées.

Cette hello de détails de document pris en charge les options de déploiement et les plateformes pour hello extension de machine virtuelle de l’Agent de l’Observateur réseau pour Windows.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation

Hello, extension de l’Agent de l’Observateur réseau pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère. Notez que hello Nano Server n’est pas prise en charge pour l’instant.

### <a name="internet-connectivity"></a>Connectivité Internet

Certaines des hello fonctionnalités de l’Agent de l’Observateur réseau exige que l’ordinateur virtuel cible hello toohello connecté Internet. Sans les connexions sortantes hello capacité tooestablish certaines des fonctionnalités de l’Agent de l’Observateur réseau hello peuvent fonctionner correctement ou deviennent indisponibles. Pour plus d’informations, consultez hello [documentation de l’Observateur réseau](../../network-watcher/network-watcher-monitoring-overview.md).

## <a name="extension-schema"></a>Schéma d’extensions

Hello JSON suivant montre schéma hello pour hello extension de l’Agent de l’Observateur réseau. extension de Hello ni requiert ni prend en charge tous les paramètres fournis par l’utilisateur pour l’instant et s’appuie sur sa configuration par défaut.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>Valeurs de propriétés

| Nom | Valeur/Exemple |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentWindows |
| typeHandlerVersion | 1.4 |


## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension de l’Agent de l’Observateur réseau pendant un déploiement de modèle Azure Resource Manager.

## <a name="powershell-deployment"></a>Déploiement PowerShell

Hello `Set-AzureRmVMExtension` commande peut être utilisé toodeploy hello Agent de l’Observateur réseau machine virtuelle extension tooan machine virtuelle existante.

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a>Résolution des problèmes et support

### <a name="troubleshooting"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello. état du déploiement hello toosee des extensions pour un ordinateur virtuel donné, hello exécution suite à l’aide de la commande hello module PowerShell Azure.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez consultez la documentation du Guide de l’utilisateur l’Observateur réseau toohello ou contactez hello Azure experts de hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
