---
title: aaaOMS extension de machine virtuelle Azure pour Linux | Documents Microsoft
description: "Déployer l’agent OMS de hello sur une machine virtuelle Linux à l’aide d’une extension de machine virtuelle."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7bbf210-7d71-4a37-ba47-9c74567a9ea6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: 0fc8003d1fae6c043eef18ae78d12f9304b70832
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="oms-virtual-machine-extension-for-linux"></a>Extension de machine virtuelle OMS pour Linux

## <a name="overview"></a>Vue d'ensemble

Operations Management Suite (OMS) fournit des fonctionnalités de surveillance, d’alerte et de correction des alertes sur le ressources cloud et locales. Hello, extension de machine virtuelle de l’Agent OMS pour Linux est publié et pris en charge par Microsoft. extension de Hello installe l’agent OMS de hello sur des machines virtuelles et inscrit les machines virtuelles dans un espace de travail OMS existant. Cette hello de détails du document prennent en charge les plateformes, les configurations et les options de déploiement pour hello extension de machine virtuelle OMS pour Linux.

## <a name="prerequisites"></a>Composants requis

### <a name="operating-system"></a>Système d’exploitation

Hello extension OMS Agent peut être exécutée sur ces distributions de Linux.

| Distribution | Version |
|---|---|
| CentOS Linux | 5, 6 et 7 |
| Oracle Linux | 5, 6 et 7 |
| Red Hat Enterprise Linux Server | 5, 6 et 7 |
| Debian GNU/Linux | 6, 7 et 8 |
| Ubuntu | 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS |
| SUSE Linux Enterprise Server | 11 et 12 |

### <a name="internet-connectivity"></a>Connectivité Internet

Hello, extension de l’Agent OMS pour Linux nécessite que l’ordinateur virtuel cible hello est connecté toohello internet. 

## <a name="extension-schema"></a>Schéma d’extensions

Hello JSON suivant montre schéma hello pour hello extension OMS Agent. extension de Hello requiert hello espace de travail et ID de clé à partir de l’espace de travail OMS de cible hello. Vous trouverez ces valeurs dans le portail OMS est hello. Étant donné que la clé d’espace de travail hello doit être traité comme des données sensibles, il doit être stocké dans une configuration protégée. Les données de paramètre d’extension protégée de machine virtuelle Azure sont chiffrées et déchiffrées uniquement sur la machine virtuelle cible hello. Notez que **workspaceId** et **workspaceKey** respectent la casse.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

### <a name="property-values"></a>Valeurs de propriétés

| Nom | Valeur/Exemple |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.EnterpriseCloud.Monitoring |
| type | OmsAgentForLinux |
| typeHandlerVersion | 1.4 |
| workspaceId (par exemple) | 6f680a37-00c6-41c7-a93f-1437e3462574 |
| workspaceKey (par exemple) | z4bU3p1/GrnWpQkky4gdabWXAhbWSTz70hm4m2Xt92XI+rSRgE8qVvRhsGo9TXffbrTahyrwv35W0pOqQAU7uQ== |


## <a name="template-deployment"></a>Déploiement de modèle

Les extensions de machines virtuelles Azure peuvent être déployées avec des modèles Azure Resource Manager. Les modèles sont idéaux lors du déploiement d’un ou plusieurs ordinateurs virtuels qui nécessitent le déploiement après la configuration tels que l’intégration tooOMS. Vous trouverez un exemple de modèle de gestionnaire de ressources qui inclut l’extension de machine virtuelle de l’Agent OMS hello sur hello [galerie de démarrage rapide Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-oms-extension-ubuntu-vm). 

configuration de JSON Hello pour une extension de machine virtuelle peut être imbriquée dans une ressource d’ordinateur virtuel hello ou placée au niveau racine de hello ou un niveau supérieur d’un modèle de gestionnaire de ressources JSON. la sélection élective Hello de configuration JSON de hello affecte la valeur hello du nom de la ressource hello et type. Pour plus d’informations, consultez [Définition du nom et du type des ressources enfants](../../azure-resource-manager/resource-manager-template-child-resource.md). 

Hello suppose extension d’OMS hello est imbriquée dans la ressource d’ordinateur virtuel hello. Lors de l’imbrication des ressources d’extension de hello, hello JSON est placée dans hello `"resources": []` objet de machine virtuelle de hello.

```json
{
  "type": "extensions",
  "name": "OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

Lorsque vous placez l’extension hello JSON au niveau racine hello du modèle de hello, nom de la ressource hello inclut un ordinateur virtuel de référence toohello parent, et type de hello reflète configuration imbriqués de hello.  

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "<parentVmResource>/OMSExtension",
  "apiVersion": "2015-06-15",
  "location": "<location>",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', <vm-name>)]"
  ],
  "properties": {
    "publisher": "Microsoft.EnterpriseCloud.Monitoring",
    "type": "OmsAgentForLinux",
    "typeHandlerVersion": "1.4",
    "settings": {
      "workspaceId": "myWorkspaceId"
    },
    "protectedSettings": {
      "workspaceKey": "myWorkSpaceKey"
    }
  }
}
```

## <a name="azure-cli-deployment"></a>Déploiement de l’interface de ligne de commande Azure

Hello CLI d’Azure peut être utilisé toodeploy hello OMS Agent VM extension tooan existant machine virtuelle. Remplacez la clé d’OMS hello et ID d’OMS avec ceux de votre espace de travail OMS. 

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.4 --protected-settings '{"workspaceKey": "omskey"}' \
  --settings '{"workspaceId": "omsid"}'
```

## <a name="troubleshoot-and-support"></a>Dépannage et support technique

### <a name="troubleshoot"></a>Résolution des problèmes

Données sur l’état de hello de déploiements d’extension peuvent être récupérées à partir de hello portail Azure et à l’aide de hello CLI d’Azure. état du déploiement hello toosee des extensions pour une machine virtuelle donnée, exécutez hello suivant à l’aide de la commande hello CLI d’Azure.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

Exécution de l’extension de sortie est journalisée toohello le fichier suivant :

```
/opt/microsoft/omsagent/bin/stdout
```

### <a name="error-codes-and-their-meanings"></a>Codes d’erreur et signification

| Code d'erreur | Signification | Action possible |
| :---: | --- | --- |
| 10 | Machine virtuelle est déjà connecté tooan espace de travail OMS | tooconnect hello VM toohello espace de travail spécifiée dans le schéma d’extension hello, définir stopOnMultipleConnections toofalse dans les paramètres publics ou supprimez cette propriété. Cette machine virtuelle est facturée une fois pour chaque espace de travail auquel elle est connectée. |
| 11 | Configuration non valide fournie toohello extension | Suivez hello précédents exemples tooset toutes les valeurs de propriété pour le déploiement. |
| 12 | Gestionnaire de package de dpkg Hello est verrouillé. | Assurez-vous que toutes les opérations de mise à jour dpkg sur l’ordinateur de hello terminés, puis réessayez. |
| 20 | Activation appelée prématurément | [Hello de mise à jour le Linux Agent Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) toohello version la plus récente. |
| 51 | Cette extension n’est pas pris en charge sur le système d’exploitation de la machine virtuelle hello | |
| 55 | Impossible de connecter le service de Microsoft Operations Management Suite toohello | Vérifiez que hello système dispose d’un accès à Internet ou qu’un proxy HTTP valide a été fourni. En outre, vérifier exactitude hello d’ID d’espace de travail hello. |

Vous trouverez des informations de dépannage supplémentaires sur hello [Guide de dépannage de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/Troubleshooting.md#).

### <a name="support"></a>Support

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure hello [forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/en-us/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/en-us/support/options/) et sélectionnez la prise en charge de Get. Pour plus d’informations sur l’utilisation de Azure prend en charge, lire hello [prise en charge de Microsoft Azure FAQ](https://azure.microsoft.com/en-us/support/faq/).
