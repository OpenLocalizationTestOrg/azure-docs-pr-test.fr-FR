---
title: aaaCustom extension de Script sur une machine virtuelle Windows | Documents Microsoft
description: "Automatiser les tâches de configuration de machine virtuelle Azure à l’aide de scripts PowerShell toorun hello Script personnalisé extension sur un ordinateur virtuel de Windows à distance"
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: ebb7340a-8f61-4d3c-a290-d7bf8de2d0bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 01/17/2017
ms.author: nepeters
ms.openlocfilehash: cf7bb895dd211f07fd010dc03b68cd77df1127b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-script-extension-for-windows-using-hello-classic-deployment-model"></a>Personnalisé Extension pour les fenêtres de Script à l’aide du modèle de déploiement classique de hello

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Extension de Script personnalisé de Hello télécharge et exécute des scripts sur les machines virtuelles. Cette extension est utile pour la configuration post-déploiement, l’installation de logiciels ou toute autre tâche de configuration ou de gestion. Scripts pouvant être téléchargés à partir de GitHub ou de stockage Azure, ou toohello portail Azure à l’extension de durée d’exécution. Hello, extension de Script personnalisé s’intègre aux modèles Azure Resource Manager et peut également être exécuté à l’aide de hello CLI d’Azure, PowerShell, portail Azure ou hello API REST de Machine virtuelle Azure.

Ce document décrit en détail comment toouse hello Extension de Script personnalisé utilisant hello module Azure PowerShell, modèles Azure Resource Manager et informations de dépannage sur les systèmes Windows.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation

Hello, Extension de Script personnalisé pour Windows puisse être exécuté sur Windows Server 2008 R2, 2012, 2012 R2 et 2016 libère.

### <a name="script-location"></a>Emplacement du script

script de Hello doit toobe stockée dans le stockage Azure, ou tout autre emplacement accessible via une URL valide.

### <a name="internet-connectivity"></a>Connectivité Internet

Hello Extension de Script personnalisé pour Windows requiert que l’ordinateur virtuel cible hello est connecté toohello internet. 

## <a name="extension-schema"></a>Schéma d’extensions

Hello JSON suivant montre schéma hello pour hello Extension de Script personnalisé. extension de Hello nécessite un emplacement de script (le stockage Azure ou un autre emplacement avec une URL valide) et un tooexecute de commande. Si vous utilisez le stockage Azure en tant que source du script hello, une clé de compte et le nom de compte stockage Azure est requise. Ces éléments doivent être considérés comme des données sensibles et spécifiés dans la configuration de paramètre protégé hello extensions. Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello.

```json
{
    "name": "config-app",
    "type": "Microsoft.ClassicCompute/virtualMachines/extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-01",
    "properties": {
        "publisher": "Microsoft.Compute",
        "extension": "CustomScriptExtension",
        "version": "1.8",
        "parameters": {
            "public": {
                "fileUris": "[myScriptLocation]"
            },
            "private": {
                "commandToExecute": "[myExecutionString]"
            }
        }
    }
}
```

### <a name="property-values"></a>Valeurs de propriétés

| Nom | Valeur/Exemple |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Compute |
| extension | CustomScriptExtension |
| typeHandlerVersion | 1.8 |
| fileUris (p. ex.) | https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1 |
| commandToExecute (p. ex.) | powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 |

## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager Extension de Script personnalisé pendant un déploiement de modèle Azure Resource Manager. Un exemple de modèle qui inclut hello Extension de Script personnalisé se trouve ici, [GitHub](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="powershell-deployment"></a>Déploiement PowerShell

Hello `Set-AzureVMCustomScriptExtension` commande peut être utilisé tooadd hello Script personnalisé extension tooan ordinateur virtuel. Pour plus d’informations, consultez [Set-AzureRmVMCustomScriptExtension](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.compute/v2.1.0/set-azurermvmcustomscriptextension).

```powershell
# create vm object
$vm = Get-AzureVM -Name 2016clas -ServiceName 2016clas1313

# set extension
Set-AzureVMCustomScriptExtension -VM $vm -FileUri myFileUri -Run 'create-file.ps1'

# update vm
$vm | Update-AzureVM
```

## <a name="troubleshoot-and-support"></a>Dépannage et support technique

### <a name="troubleshoot"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide du module Azure PowerShell de hello. état du déploiement toosee hello des extensions pour une machine virtuelle donnée, exécutez hello commande suivante.

```powershell
Get-AzureVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Exécution de l’extension de sortie nous toofiles connecté trouvé dans hello suivant de répertoire de la machine virtuelle cible hello.

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Compute.CustomScriptExtension
```

script Hello proprement dit est téléchargé dans hello suivant de répertoire de la machine virtuelle cible hello.

```cmd
C:\Packages\Plugins\Microsoft.Compute.CustomScriptExtension\1.*\Downloads
```

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
