---
title: "Créer une machine virtuelle Linux dans Azure à partir d’un modèle | Documents Microsoft"
description: "Comment utiliser Azure CLI 2.0 pour créer une machine virtuelle Linux à partir d’un modèle Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 09/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 938304efe5e4a13736a50348bd0531c475149aec
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Comment créer une machine virtuelle Linux avec des modèles Azure Resource Manager
Cet article montre comment déployer rapidement une machine virtuelle Linux avec des modèles Azure Resource Manager et Azure CLI 2.0. Vous pouvez également effectuer ces étapes à l’aide [d’Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Vue d’ensemble des modèles
Les modèles Azure Resource Manager sont des fichiers JSON qui définissent l’infrastructure et la configuration de votre solution Azure. Un modèle vous permet de déployer votre solution à plusieurs reprises tout au long de son cycle de vie pour avoir la garantie que vos ressources présentent un état cohérent lors de leur déploiement. Pour en savoir plus sur le format du modèle et la manière de le construire, voir [Créer votre premier modèle Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Pour afficher la syntaxe JSON pour les types de ressources, voir [Définir des ressources dans les modèles Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Créer un groupe de ressources
Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. Un groupe de ressources doit être créé avant les machines virtuelles. L’exemple suivant crée un groupe de ressources nommé *myResourceGroupVM* dans la région *eastus* :

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine
L’exemple suivant crée une machine virtuelle à partir de [ce modèle Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) à l’aide du script [az group deployment create](/cli/azure/group/deployment#create). Fournissez la valeur de votre propre clé publique SSH, telle que le contenu de *~/.ssh/id_rsa.pub*. Si vous devez créer une paire de clés SSH, voir [Comment créer et utiliser une paire de clés SSH pour des machines virtuelles Linux dans Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

Dans cet exemple, vous avez spécifié un modèle stocké dans GitHub. Vous pouvez également télécharger ou créer un modèle, et spécifier le chemin d’accès local avec le même paramètre `--template-file`.

Pour établir une connexion SSH à votre machine virtuelle, obtenez l’adresse IP publique avec le script [az network public-ip show](/cli/azure/network/public-ip#show) :

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Vous pouvez ensuite établir une connexion SSH à votre machine virtuelle comme d’habitude. Indiquez votre propre adresse IP publique à partir de la commande précédente :

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez créé une machine virtuelle Linux de base. Pour d’autres modèles Resource Manager qui incluent des infrastructures d’applications ou créent des environnements plus complexes, parcourez la [galerie de modèles de démarrage rapide Microsoft Azure](https://azure.microsoft.com/documentation/templates/).