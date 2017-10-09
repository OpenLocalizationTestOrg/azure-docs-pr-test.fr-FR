---
title: "aaaAzure Extension de Script personnalisé pour Windows | Documents Microsoft"
description: "Automatiser les tâches de configuration de machine virtuelle Windows à l’aide d’extension de Script personnalisé hello"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f4181fee-7a9d-4a1c-b517-52956f5b7fa1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/16/2017
ms.author: nepeters
ms.openlocfilehash: 97e065242e9fed116ee20b074f4e302a0cd10585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows"></a>Extension de script personnalisé pour Windows

Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles. Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion. Scripts pouvant être téléchargés à partir de GitHub ou de stockage Azure, ou toohello portail Azure à l’extension de durée d’exécution. Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.

Ce document décrit en détail comment toouse hello Extension de Script personnalisé utilisant hello module Azure PowerShell, modèles Azure Resource Manager et informations de dépannage sur les systèmes Windows.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation

Hello, Extension de Script personnalisé pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.

### <a name="script-location"></a>Emplacement du script

script de Hello doit toobe stockée dans le stockage Blob Azure, ou tout autre emplacement accessible via une URL valide.

### <a name="internet-connectivity"></a>Connectivité Internet

Hello Extension de Script personnalisé pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet. 

## <a name="extension-schema"></a>Schéma d’extensions

Hello JSON suivant montre schéma hello pour hello Extension de Script personnalisé. extension de Hello nécessite un emplacement de script (le stockage Azure ou un autre emplacement avec une URL valide) et un tooexecute de commande. Si vous utilisez le stockage Azure en tant que source du script hello, une clé de compte et le nom de compte stockage Azure est requise. Ces éléments doivent être considérés comme des données sensibles et spécifiés dans la configuration de paramètre protégé hello extensions. Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
        "[variables('musicstoresqlName')]"
    ],
    "tags": {
        "displayName": "config-app"
    },
    "properties": {
        "publisher": "Microsoft.Compute",
        "type": "CustomScriptExtension",
        "typeHandlerVersion": "1.9",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "fileUris": [
                "script location"
            ]
        },
        "protectedSettings": {
            "commandToExecute": "myExecutionCommand",
            "storageAccountName": "myStorageAccountName",
            "storageAccountKey": "myStorageAccountKey"
        }
    }
}
```

### <a name="property-values"></a>Valeurs de propriétés

| Nom | Valeur/Exemple |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| type | extensions |
| typeHandlerVersion | 1.9 |
| fileUris (p. ex.) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (p. ex.) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |
| storageAccountName (p. ex.) | examplestorageacct |
| storageAccountKey (p. ex.) | TmJK/1N3AbAZ3q/+hOXoi/l73zOqsaxXDhqa9Y83/v5UpXQp2DQIBuv2Tifp60cE/OaHsJZmQZ7teQfczQj8hg== |

**Remarque** : ces noms de propriété respectent la casse. Utiliser des noms de hello comme indiqué ci-dessus tooavoid les problèmes de déploiement.

## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager Extension de Script personnalisé pendant un déploiement de modèle Azure Resource Manager. Un exemple de modèle qui inclut hello Extension de Script personnalisé se trouve ici, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Déploiement PowerShell

Hello `Set-AzureRmVMCustomScriptExtension` commande peut être utilisé tooadd hello Script personnalisé extension tooan ordinateur virtuel. Pour plus d’informations, consultez [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).
```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName myResourceGroup `
    -VMName myVM `
    -Location myLocation `
    -FileUri myURL `
    -Run 'myScript.ps1' `
    -Name DemoScriptExtension
```

## <a name="troubleshoot-and-support"></a>Dépannage et support technique

### <a name="troubleshoot"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello. état du déploiement toosee hello des extensions pour une machine virtuelle donnée, exécutez hello commande suivante.

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Exécution de l’extension de sortie est toofiles connecté sous hello suivant active sur la machine virtuelle cible hello.
```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

Hello spécifié les fichiers sont téléchargés dans hello suivant de répertoire de la machine virtuelle cible hello.
```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads\<n>
```
où `<n>` est un entier décimal qui peut-être changer entre les exécutions de l’extension de hello.  Hello `1.*` valeur correspond à celle en cours réel, de hello `typeHandlerVersion` valeur de l’extension hello.  Par exemple, le répertoire réels de hello peut être `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2`.  

Lors de l’exécution hello `commandToExecute` commande, extension de hello ont définira ce répertoire (par exemple, `...\Downloads\2`) en tant que répertoire de travail actuel hello. Cette utilisation de hello permet des fichiers de chemins d’accès relatifs toolocate hello téléchargés via hello `fileURIs` propriété. Consultez le tableau hello ci-dessous pour obtenir des exemples.

Étant donné que le chemin d’accès absolu de téléchargement de hello peut varier au fil du temps, il s’agit d’une meilleure tooopt des chemins d’accès/fichier de script relatif Bonjour `commandToExecute` de chaîne, chaque fois que possible. Par exemple :
```json
    "commandToExecute": "powershell.exe . . . -File './scripts/myscript.ps1'"
```

Les informations de chemin d’accès après le premier segment URI hello est conservé pour les fichiers téléchargés via hello `fileUris` liste de propriétés.  Comme indiqué dans le tableau hello ci-dessous, les fichiers téléchargés sont mappés à structure de téléchargement dans les sous-répertoires tooreflect hello Hello `fileUris` valeurs.  

#### <a name="examples-of-downloaded-files"></a>Exemples de fichiers téléchargés

| URI dans fileUris | Emplacement téléchargé relatif | Emplacement téléchargé absolu* |
| ---- | ------- |:--- |
| `https://someAcct.blob.core.windows.net/aContainer/scripts/myscript.ps1` | `./scripts/myscript.ps1` |`C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\scripts\myscript.ps1`  |
| `https://someAcct.blob.core.windows.net/aContainer/topLevel.ps1` | `./topLevel.ps1` | `C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.8\Downloads\2\topLevel.ps1` |

\*Comme ci-dessus, chemins d’accès du répertoire absolu hello change sur la durée de vie hello Hello machine virtuelle, mais pas dans une seule exécution de l’extension CustomScript de hello.

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et Stack Overflow] (https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
