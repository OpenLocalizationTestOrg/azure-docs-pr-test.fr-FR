---
title: "fonctionnalités et extensions de l’ordinateur aaaVirtual pour Linux | Documents Microsoft"
description: "Découvrez les extensions disponibles pour les machines virtuelles, regroupées par ce qu’ils fournissent ou améliorent."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Extensions et fonctionnalités de machine virtuelle pour Linux

Les extensions de machine virtuelle Azure sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure. Par exemple, si un ordinateur virtuel requiert l’installation du logiciel, de protection antivirus ou de configuration de Docker, une extension de machine virtuelle peut être utilisé toocomplete ces tâches. Les extensions de machine virtuelle Azure peuvent être exécutées à l’aide de hello CLI d’Azure PowerShell, les modèles Azure Resource Manager et hello portail Azure. Les extensions peuvent être associées à un nouveau déploiement de machine virtuelle ou s’exécuter sur tout système existant.

Ce document fournit une vue d’ensemble des extensions de machine virtuelle, les conditions préalables pour l’utilisation des extensions de machine virtuelle Azure et de conseils toodetect, gérer et supprimer des extensions de machine virtuelle. Ce document fournit des informations générales, car de nombreuses extensions de machine virtuelle sont disponibles, chacune présentant une configuration potentiellement unique. Vous trouverez plus d’informations spécifiques à l’extension dans chaque document spécifique toohello individuels d’extension.

## <a name="use-cases-and-samples"></a>Cas d’utilisation et exemples

Plusieurs extensions de machine virtuelle Azure sont disponibles, chacune impliquant un cas d’utilisation spécifique. Voici quelques exemples :

- Appliquer l’état souhaité de PowerShell configurations tooa machine virtuelle hello extension DSC pour Linux. Pour plus d’informations sur l’extension DSC Azure, consultez [cette page](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Configurer la surveillance d’un ordinateur virtuel avec hello extension de machine virtuelle l’Agent de surveillance de Microsoft. Pour plus d’informations, consultez [comment toomonitor un VM Linux](tutorial-monitoring.md).
- Configurer la surveillance de votre infrastructure d’Azure avec hello Datadog extension. Pour plus d’informations, consultez hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configurer un hôte Docker sur une machine virtuelle Azure à l’aide d’extension de machine virtuelle de Docker hello. Pour plus d’informations sur l’extension de machine virtuelle Docker, consultez [cet article](dockerextension.md).

En outre extensions tooprocess spécifiques, une extension de Script personnalisé est disponible pour les machines virtuelles Windows et Linux. Hello, extension de Script personnalisé pour Linux permet de n’importe quel toobe de script d’interpréteur de commandes s’exécutent sur un ordinateur virtuel. Les scripts personnalisés s’avèrent utile pour concevoir des déploiements Azure qui nécessitent une configuration plus avancée que celle fournie par les outils Azure natifs. Pour plus d’informations sur l’extension de script personnalisé pour les machines virtuelles Linux, consultez [cet article](extensions-customscript.md).


## <a name="prerequisites"></a>Composants requis

Chaque extension de machine virtuelle peut présenter son propre ensemble de composants requis. Par exemple, hello extension de machine virtuelle de Docker a une condition préalable d’une distribution Linux pris en charge. Configuration requise des extensions individuelles est détaillées dans la documentation spécifique à l’extension de hello.

### <a name="azure-vm-agent"></a>Agent de machine virtuelle Azure

agent de machine virtuelle Azure Hello gère les interactions entre une machine virtuelle Azure et le contrôleur de structure Azure hello. agent de machine virtuelle Hello est chargé de nombreux aspects fonctionnels de déploiement et la gestion des machines virtuelles Azure, y compris les extensions de machine virtuelle en cours d’exécution. l’agent de machine virtuelle Azure Hello est préinstallé sur les images Azure Marketplace et peut être installé manuellement sur les systèmes d’exploitation pris en charge.

Pour plus d’informations sur les systèmes d’exploitation pris en charge et sur la procédure d’installation, consultez l’article [Agent de machine virtuelle et extensions Azure](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Détecter les extensions de machine virtuelle

De nombreuses extensions de machine virtuelle différentes peuvent être utilisées avec les machines virtuelles Azure. toosee une liste complète, exécutez hello suivant de commande avec hello CLI d’Azure, le remplacement d’emplacement d’exemple hello avec emplacement hello de votre choix.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Exécuter les extensions de machine virtuelle

Extensions de machine virtuelle Azure peuvent être exécutées sur des machines virtuelles existantes, qui sont utiles lorsque vous avez besoin de modifications de configuration toomake ou restaurer la connectivité sur une machine virtuelle déjà déployée. Les extensions de machines virtuelles peuvent également être intégrées dans des déploiements de modèles Azure Resource Manager. L’utilisation d’extensions avec des modèles Resource Manager permet de déployer et de configurer des machines virtuelles Azure sans avoir à intervenir après le déploiement.

Hello méthodes suivantes peut être utilisée toorun une extension sur un ordinateur virtuel existant.

### <a name="azure-cli"></a>Interface de ligne de commande Azure

Extensions de machine virtuelle Azure peuvent être exécutées sur un ordinateur virtuel existant à l’aide de hello `az vm extension set` commande. Cet exemple exécute une extension de script personnalisé hello contre un ordinateur virtuel.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Hello script produit la sortie similaire toohello suivant du texte :

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Portail Azure

Extensions de machine virtuelle peuvent être appliqué tooan une machine virtuelle existante via hello portail Azure. toodo par conséquent, activez la machine virtuelle de hello, choisissez **Extensions**, puis cliquez sur **ajouter**. Sélectionnez l’extension hello souhaité à partir de la liste de hello d’extensions disponibles et suivez les instructions hello dans l’Assistant de hello.

Hello image suivante montre installation hello Hello extension de Script personnalisé de Linux à partir de hello portail Azure.

![Installer l’extension de script personnalisé](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Modèles Microsoft Azure Resource Manager

Extensions de machine virtuelle peuvent être ajoutée tooan Azure Resource Manager modèle et exécutée avec un déploiement hello du modèle de hello. Lorsque vous déployez une extension avec un modèle, vous pouvez créer des déploiements Azure entièrement configurés. Par exemple, hello que JSON suivant est tiré d’un modèle de gestionnaire de ressources. modèle de Hello déploie un ensemble de l’équilibrage de la charge des machines virtuelles et d’une base de données SQL Azure et installe une application .NET Core sur chaque machine virtuelle. prend en charge de l’installation du logiciel hello Hello extension de machine virtuelle.

Pour plus d’informations, consultez hello complète [modèle Resource Manager](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Pour plus d’informations, consultez [Création de modèles Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Sécuriser les données des extensions de machine virtuelle

Lorsque vous exécutez une extension de machine virtuelle, il peut être nécessaire de tooinclude des informations sensibles telles que les informations d’identification, les noms de compte de stockage et les clés d’accès de compte de stockage. Plusieurs extensions de machine virtuelle incluent une configuration protégée qui chiffre les données et la déchiffre uniquement à l’intérieur de la machine virtuelle cible hello. Chaque extension possède un schéma spécifique de configuration protégée, présenté en détail dans la documentation consacrée à l’extension.

Bonjour à l’exemple suivant montre une instance de hello extension de Script personnalisé pour Linux. Notez que tooexecute de commande hello comprend un ensemble d’informations d’identification. Dans cet exemple, hello commande tooexecute n’est pas chiffrée.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Déplacement hello **commande tooexecute** propriété toohello **protégé** configuration sécurise la chaîne de l’exécution de hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Résoudre les problèmes liés aux extensions de machine virtuelle

Chaque extension de machine virtuelle peut avoir l’extension de toohello spécifique d’étapes de résolution des problèmes. Par exemple, lorsque vous utilisez l’extension de Script personnalisé hello, détails de l’exécution de script sont accessibles localement sur l’ordinateur virtuel de hello sur lequel l’extension de hello a été exécutée. La procédure de résolution des problèmes spécifique d’une extension est présentée en détail dans la documentation de cette dernière.

Hello suivant les étapes de dépannage s’appliquent à des extensions de machine virtuelle tooall.

### <a name="view-extension-status"></a>Afficher l’état de l’extension

Une fois une extension de machine virtuelle a été exécutée sur un ordinateur virtuel, utilisez hello suivant l’état de l’extension tooreturn commande CLI d’Azure. Remplacez les exemples de noms de paramètre par vos propres valeurs.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

sortie de Hello ressemble à hello suivant du texte :

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

État d’exécution de l’extension peut également trouver dans hello portail Azure. état de hello tooview d’extension, sélectionnez hello virtual machine, choisissez **Extensions**, et sélectionnez hello extension souhaitée.

### <a name="rerun-a-vm-extension"></a>Réexécuter une extension de machine virtuelle

Il peut y avoir des cas dans lesquels une extension de machine virtuelle doit toobe exécuter à nouveau. Vous pouvez réexécuter une extension en le supprimant, puis en réexécutant les extension hello avec une méthode d’exécution de votre choix. tooremove une extension, exécutez hello suivant de commande avec hello CLI d’Azure. Remplacez les exemples de noms de paramètre par vos propres valeurs.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Vous pouvez supprimer une extension à l’aide de hello Bonjour portail Azure comme suit :

1. Sélectionnez une machine virtuelle.
2. Choisissez **Extensions**.
3. Sélectionnez l’extension hello souhaité.
4. Choisissez **Désinstaller**.

## <a name="common-vm-extension-reference"></a>Informations de référence sur les extensions de machine virtuelle courantes
| Nom de l’extension | Description | Plus d’informations |
| --- | --- | --- |
| Extension de script personnalisé pour Linux |Exécuter des scripts sur une machine virtuelle Azure |[Extension de script personnalisé pour Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extension Docker |Installez hello Docker démon toosupport à distance les commandes Docker. |[Extension de machine virtuelle Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extension d’accès aux machines virtuelles |Récupérer l’accès tooan machine virtuelle Azure |[Extension d’accès aux machines virtuelles](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Extension Diagnostics Azure |Gérer les diagnostics Azure |[Extension Diagnostics Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extension d’accès aux machines virtuelles Azure |Gérer les utilisateurs et les informations d’identification |[Extension d’accès aux machines virtuelles pour Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
