---
title: "fonctionnalités et extensions de l’ordinateur aaaVirtual pour Windows dans Azure | Documents Microsoft"
description: "Découvrez les extensions disponibles pour les machines virtuelles, regroupées par ce qu’ils fournissent ou améliorent."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 999d63ee-890e-432e-9391-25b3fc6cde28
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/06/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 61ccfd696b38e9be1026d836d5796c2346fd650f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-windows"></a>Extensions et fonctionnalités de machine virtuelle pour Windows

Les extensions de machine virtuelle Azure sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure. Par exemple, si un ordinateur virtuel requiert l’installation du logiciel, de protection antivirus ou de configuration de Docker, une extension de machine virtuelle peut être utilisé toocomplete ces tâches. Les extensions de machine virtuelle Azure peuvent être exécutées à l’aide de hello CLI d’Azure PowerShell, les modèles Azure Resource Manager et hello portail Azure. Les extensions peuvent être associées à un nouveau déploiement de machine virtuelle ou s’exécuter sur tout système existant.

Ce document fournit une vue d’ensemble des extensions de machine virtuelle, les conditions préalables pour l’utilisation des extensions de machine virtuelle et de conseils toodetect, gérer et supprimer des extensions de machine virtuelle. Ce document fournit des informations générales, car de nombreuses extensions de machine virtuelle sont disponibles, chacune présentant une configuration potentiellement unique. Vous trouverez plus d’informations spécifiques à l’extension dans chaque document spécifique toohello individuels d’extension.

## <a name="use-cases-and-samples"></a>Cas d’utilisation et exemples

Plusieurs extensions de machine virtuelle Azure sont disponibles, chacune impliquant un cas d’utilisation spécifique. Exemples de cas d’utilisation :

- Appliquer l’état souhaité de PowerShell configurations tooa virtual machine pour Windows à l’aide d’extension de hello DSC. Pour plus d’informations sur l’extension DSC Azure, consultez [cette page](extensions-dsc-overview.md).
- Configurer la surveillance de machine virtuelle à l’aide d’extension de VM de l’Agent de surveillance Microsoft hello. Pour plus d’informations, consultez [tooLog de machines virtuelles Azure de se connecter Analytique](../../log-analytics/log-analytics-azure-vm-extension.md).
- Configurer la surveillance de votre infrastructure d’Azure avec hello Datadog extension. Pour plus d’informations, consultez hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configurer une machine virtuelle Azure à l’aide de Chef. Pour plus d’informations, consultez [Automatisation du déploiement de machine virtuelle Azure avec Chef](chef-automation.md).

En outre extensions tooprocess spécifiques, une extension de Script personnalisé est disponible pour les machines virtuelles Windows et Linux. Hello extension de Script personnalisé pour Windows permet à n’importe quel toobe de script PowerShell s’exécutent sur un ordinateur virtuel. Cela s’avère utile pour concevoir des déploiements Azure qui nécessitent une configuration plus avancée que celle permise par les outils Azure. Pour plus d’informations sur l’extension de script personnalisé pour les machines virtuelles Windows, consultez [cet article](extensions-customscript.md).


## <a name="prerequisites"></a>Composants requis

Chaque extension de machine virtuelle peut présenter son propre ensemble de composants requis. Par exemple, hello extension de machine virtuelle de Docker a une condition préalable d’une distribution Linux pris en charge. Configuration requise des extensions individuelles est détaillées dans la documentation spécifique à l’extension de hello.

### <a name="azure-vm-agent"></a>Agent de machine virtuelle Azure
l’agent de machine virtuelle Azure Hello gère l’interaction entre une machine virtuelle Azure et le contrôleur de structure Azure hello. agent de machine virtuelle Hello est chargé de nombreux aspects fonctionnels de déploiement et la gestion des machines virtuelles Azure, y compris les extensions de machine virtuelle en cours d’exécution. l’agent de machine virtuelle Azure Hello est préinstallé sur les images Azure Marketplace et peut être installé sur les systèmes d’exploitation pris en charge.

Pour plus d’informations sur les systèmes d’exploitation pris en charge et sur la procédure d’installation, consultez l’article [Agent de machine virtuelle et extensions Azure](agent-user-guide.md).

## <a name="discover-vm-extensions"></a>Détecter les extensions de machine virtuelle
De nombreuses extensions de machine virtuelle différentes peuvent être utilisées avec les machines virtuelles Azure. toosee une liste complète, exécutez hello commande avec le module de hello Azure Resource Manager PowerShell suivante. Transformer en emplacement de hello souhaité toospecify que lorsque vous exécutez cette commande.

```powershell
Get-AzureRmVmImagePublisher -Location WestUS | `
Get-AzureRmVMExtensionImageType | `
Get-AzureRmVMExtensionImage | Select Type, Version
```

## <a name="run-vm-extensions"></a>Exécuter les extensions de machine virtuelle

Extensions de machine virtuelle Azure peuvent être exécutées sur des ordinateurs virtuels existants, ce qui est utile lorsque vous avez besoin de modifications de configuration toomake ou restaurer la connectivité sur une machine virtuelle déjà déployée. Les extensions de machines virtuelles peuvent également être intégrées dans des déploiements de modèles Azure Resource Manager. À l’aide des extensions avec des modèles de gestionnaire de ressources, vous pouvez activer toobe de machines virtuelles déployés et configurés sans hello intervention de post-déploiement.

Hello méthodes suivantes peut être utilisée toorun une extension sur un ordinateur virtuel existant.

### <a name="powershell"></a>PowerShell

Il existe plusieurs commandes PowerShell pour l’exécution des extensions. toosee obtenir la liste, exécutez hello suivant de commandes PowerShell.

```powershell
get-command Set-AzureRM*Extension* -Module AzureRM.Compute
```

Cela fournit suivant toohello similaire de sortie :

```powershell
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Set-AzureRmVMAccessExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMADDomainExtension                     2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMAEMExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBackupExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMBginfoExtension                       2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMChefExtension                         2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMCustomScriptExtension                 2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiagnosticsExtension                  2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDiskEncryptionExtension               2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMDscExtension                          2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMExtension                             2.2.0      AzureRM.Compute
Cmdlet          Set-AzureRmVMSqlServerExtension                    2.2.0      AzureRM.Compute
```

Hello exemple suivant utilise toodownload extension de Script personnalisé hello un script à partir d’un référentiel GitHub sur la machine virtuelle cible hello et puis exécutez le script de hello. Pour plus d’informations sur l’extension de Script personnalisé de hello, consultez [vue d’ensemble des extensions de Script personnalisé](extensions-customscript.md).

```powershell
Set-AzureRmVMCustomScriptExtension -ResourceGroupName "myResourceGroup" `
    -VMName "myVM" -Name "myCustomScript" `
    -FileUri "https://raw.githubusercontent.com/neilpeterson/nepeters-azure-templates/master/windows-custom-script-simple/support-scripts/Create-File.ps1" `
    -Run "Create-File.ps1" -Location "West US"
```

Dans cet exemple, hello extension d’accès de la machine virtuelle est le mot de passe utilisé tooreset hello d’administration d’une machine virtuelle Windows. Pour plus d’informations sur hello extension d’accès de la machine virtuelle, consultez [service réinitialiser le Bureau à distance dans une machine virtuelle Windows](reset-rdp.md).

```powershell
$cred=Get-Credential

Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" -Name "myVMAccess" `
    -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

Hello `Set-AzureRmVMExtension` commande peut être utilisé toostart n’importe quelle extension de machine virtuelle. Pour plus d’informations, consultez hello [Set-AzureRmVMExtension référence](https://msdn.microsoft.com/en-us/library/mt603745.aspx).


### <a name="azure-portal"></a>Portail Azure

Une extension de machine virtuelle peut être appliqué tooan une machine virtuelle existante via hello portail Azure. toodo par conséquent, activez la machine virtuelle de hello vous souhaitez toouse, choisissez **Extensions**, puis cliquez sur **ajouter**. La liste des extensions disponibles s’affiche. Sélectionnez hello une souhaité et suivez les étapes de hello dans l’Assistant de hello.

Hello image suivante montre installation hello Hello extension Microsoft Antimalware de hello portail Azure.

![Installer l’extension Antimalware](./media/extensions-features/installantimalwareextension.png)

### <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager

Extensions de machine virtuelle peuvent être ajoutée tooan Azure Resource Manager modèle et exécutée avec un déploiement hello du modèle de hello. Le déploiement d’extensions avec un modèle permet de créer des déploiements Azure entièrement configurés. Par exemple, hello que JSON suivant est tiré d’un modèle de gestionnaire de ressources qui déploie un ensemble de l’équilibrage de la charge des machines virtuelles et d’une base de données SQL Azure, puis installe une application .NET Core sur chaque machine virtuelle. prend en charge de l’installation du logiciel hello Hello extension de machine virtuelle.

Pour plus d’informations, consultez hello [modèle de gestionnaire de ressources complet](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Pour plus d’informations, consultez l’article [Création de modèles Azure Resource Manager avec des extensions de machine virtuelle Windows](template-description.md#extensions).

## <a name="secure-vm-extension-data"></a>Sécuriser les données des extensions de machine virtuelle

Lorsque vous exécutez une extension de machine virtuelle, il peut être nécessaire de tooinclude des informations sensibles telles que les informations d’identification, les noms de compte de stockage et les clés d’accès de compte de stockage. Plusieurs extensions de machine virtuelle incluent une configuration protégée qui chiffre les données et la déchiffre uniquement à l’intérieur de la machine virtuelle cible hello. Chaque extension possède un schéma spécifique de configuration protégée qui sera présenté en détail dans la documentation consacrée à l’extension.

Bonjour à l’exemple suivant montre une instance de hello extension de Script personnalisé pour Windows. Notez que tooexecute de commande hello comprend un ensemble d’informations d’identification. Dans cet exemple, hello commande tooexecute n’est pas chiffrée.


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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ],
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

Protéger la chaîne de l’exécution de hello en déplaçant hello **commande tooexecute** propriété toohello **protégé** configuration.

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
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
    }
}
```

## <a name="troubleshoot-vm-extensions"></a>Résoudre les problèmes liés aux extensions de machine virtuelle

Chaque extension de machine virtuelle peut présenter une procédure de résolution des problèmes spécifique. Par exemple, lorsque vous utilisez l’extension de Script personnalisé hello, détails de l’exécution de script sont accessibles localement sur l’ordinateur virtuel de hello sur lequel l’extension de hello a été exécutée. La procédure de résolution des problèmes spécifique d’une extension est présentée en détail dans la documentation de cette dernière.

Hello suivant les étapes de dépannage s’appliquent à des extensions de machine virtuelle tooall.

### <a name="view-extension-status"></a>Afficher l’état de l’extension

Une fois une extension de machine virtuelle a été exécutée sur un ordinateur virtuel, utilisez hello suivant l’état de l’extension tooreturn commande PowerShell. Remplacez les exemples de noms de paramètre par vos propres valeurs. Hello `Name` paramètre prend le nom hello toohello extension au moment de l’exécution.

```PowerShell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

sortie de Hello ressemble à hello suivantes :

```json
ResourceGroupName       : myResourceGroup
VMName                  : myVM
Name                    : myExtensionName
Location                : westus
Etag                    : null
Publisher               : Microsoft.Azure.Extensions
ExtensionType           : DockerExtension
TypeHandlerVersion      : 1.0
Id                      : /subscriptions/mySubscriptionIS/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM/extensions/myExtensionName
PublicSettings          :
ProtectedSettings       :
ProvisioningState       : Succeeded
Statuses                :
SubStatuses             :
AutoUpgradeMinorVersion : False
ForceUpdateTag          :
```

État d’exécution de l’extension peut également trouver dans hello portail Azure. état de hello tooview d’extension, sélectionnez hello virtual machine, choisissez **Extensions**, et sélectionnez hello extension souhaitée.

### <a name="rerun-vm-extensions"></a>Réexécuter les extensions de machine virtuelle

Il peut y avoir des cas dans lesquels une extension de machine virtuelle doit toobe exécuter à nouveau. Pour cela, en supprimant hello extension, puis en réexécutant les extension hello avec une méthode d’exécution de votre choix. tooremove une extension, exécutez hello commande avec le module de hello Azure PowerShell suivante. Remplacez les exemples de noms de paramètre par vos propres valeurs.

```powershell
Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -VMName myVM -Name myExtensionName
```

Une extension peut également être supprimée à l’aide de hello portail Azure. toodo pour :

1. Sélectionnez une machine virtuelle.
2. Sélectionnez **Extensions**.
3. Choisissez les extension hello souhaité.
4. Sélectionnez **Désinstaller**.

## <a name="common-vm-extensions-reference"></a>Informations de référence sur les extensions de machine virtuelle courantes
| Nom de l’extension | Description | Plus d’informations |
| --- | --- | --- |
| Extension de script personnalisé pour Windows |Exécuter des scripts sur une machine virtuelle Azure |[Extension de script personnalisé pour Windows](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extension DSC pour Windows |Extension PowerShell DSC (Desired State Configuration, configuration d’état souhaité) |[Extension DSC pour Windows](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Extension Diagnostics Azure |Gérer les diagnostics Azure |[Extension Diagnostics Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extension d’accès aux machines virtuelles Azure |Gérer les utilisateurs et les informations d’identification |[Extension d’accès aux machines virtuelles pour Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
