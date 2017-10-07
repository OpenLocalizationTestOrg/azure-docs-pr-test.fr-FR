---
title: "aaaAzure extension de machine virtuelle de l’Agent de l’Observateur réseau pour Linux | Documents Microsoft"
description: "Déployer hello Agent de l’Observateur réseau sur une machine virtuelle Linux à l’aide d’une extension de machine virtuelle."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Extension de machine virtuelle Agent Network Watcher pour Linux

## <a name="overview"></a>Vue d'ensemble

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) est un service d’analyse, de diagnostic et d’analytique des performances réseau permettant de surveiller les réseaux Azure. Hello, extension de machine virtuelle de l’Agent de l’Observateur réseau est obligatoire pour certaines des fonctionnalités de l’Observateur réseau hello sur des machines virtuelles. notamment la capture du trafic réseau à la demande et d’autres fonctionnalités avancées.

Cette hello de détails de document pris en charge les options de déploiement et les plateformes pour hello extension de machine virtuelle de l’Agent de l’Observateur réseau pour Linux.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation

Hello, extension de l’Agent de l’Observateur réseau peut être exécutée sur ces distributions de Linux :

| Distribution | Version |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS et 12.04 LTS |
| Debian | 7 et 8 |
| Red Hat | 6.x et 7.x |
| Oracle Linux | 7x |
| SUSE | 11 et 12 |
| openSUSE | 7.0 |
| CentOS | 7.0 |

Remarque : CoreOS n’est pas pris en charge pour le moment.

### <a name="internet-connectivity"></a>Connectivité Internet

Certaines des hello fonctionnalités de l’Agent de l’Observateur réseau exige que l’ordinateur virtuel cible hello toohello connecté Internet. Sans les connexions sortantes hello capacité tooestablish certaines des fonctionnalités de l’Agent de l’Observateur réseau hello peuvent fonctionner correctement ou deviennent indisponibles. Pour plus d’informations, consultez hello [documentation de l’Observateur réseau](https://review.docs.microsoft.com/en-us/azure/network-watcher/).

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
        "type": "NetworkWatcherAgentLinux",
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
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. schéma JSON de Hello détaillé dans la section précédente de hello peut être utilisé dans un hello toorun du modèle Azure Resource Manager extension de l’Agent de l’Observateur réseau pendant un déploiement de modèle Azure Resource Manager.

## <a name="azure-cli-deployment"></a>Déploiement de l’interface de ligne de commande Azure

Hello CLI d’Azure peut être utilisé toodeploy hello réseau Observateur l’Agent VM extension tooan existant machine virtuelle.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>Résolution des problèmes et support

### <a name="troubleshooting"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide de hello CLI d’Azure. état du déploiement hello toosee des extensions pour une machine virtuelle donnée, exécutez hello suivant à l’aide de la commande hello CLI d’Azure.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

Exécution de l’extension de sortie est journalisée toofiles trouvé dans hello suivant active :

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez consultez la documentation de l’Observateur réseau toohello ou contactez hello Azure experts de hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
