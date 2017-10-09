---
title: "aaaCreate un VM Linux dans Azure à partir d’un modèle | Documents Microsoft"
description: "Comment toouse hello Azure CLI 2.0 toocreate un VM Linux à partir d’un modèle de gestionnaire de ressources"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Comment toocreate une machine virtuelle Linux modèles Azure Resource Manager
Cet article vous explique comment tooquickly déployer un ordinateur virtuel de Linux (VM) avec les modèles Azure Resource Manager et hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Vue d’ensemble des modèles
Les modèles de gestionnaire de ressources Azure sont des fichiers JSON qui définissent l’infrastructure de hello et la configuration de votre solution Azure. Un modèle vous permet de déployer votre solution à plusieurs reprises tout au long de son cycle de vie pour avoir la garantie que vos ressources présentent un état cohérent lors de leur déploiement. toolearn en savoir plus sur le format de hello du modèle de hello et comment vous construisez, consultez [créer votre premier modèle Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). tooview hello syntaxe JSON pour les types de ressources, consultez [définir des ressources dans les modèles Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Créer un groupe de ressources
Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant les machines virtuelles. Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupVM* Bonjour *eastus* région :

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine
Hello exemple suivant crée une machine virtuelle à partir de [ce modèle Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create). Fournissez une valeur de hello de votre propre clé publique SSH, telles que du contenu hello de *~/.ssh/id_rsa.pub*. Si vous devez toocreate une paire de clés SSH, consultez [comment toocreate et utilisez un SSH paire de clés pour les machines virtuelles dans Azure Linux](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

Dans cet exemple, vous avez spécifié un modèle stocké dans GitHub. Vous pouvez également télécharger ou créer un modèle et spécifiez le chemin d’accès local de hello avec hello même `--template-file` paramètre.

tooSSH tooyour machine virtuelle, obtenir l’adresse IP publique de hello avec [az réseau public-ip afficher](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Vous pouvez ensuite SSH tooyour VM normalement :

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez créé une machine virtuelle Linux de base. D’autres modèles de gestionnaire de ressources qui incluent des infrastructures d’applications ou de créer des environnements plus complexes, parcourir hello [galerie de modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/).
