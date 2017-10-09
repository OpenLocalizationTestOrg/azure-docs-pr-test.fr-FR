---
title: "images de machine virtuelle personnalisées aaaCreate avec hello CLI d’Azure | Documents Microsoft"
description: "Didacticiel : créer une image de machine virtuelle personnalisée à l’aide de hello CLI d’Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Créer une image personnalisée d’une machine virtuelle de Azure à l’aide de hello CLI

Les images personnalisées sont comme des images de la Place de marché, sauf que vous les créez vous-même. Images personnalisées peuvent être des configurations toobootstrap utilisés tels que le préchargement des applications, les configurations de l’application et les autres configurations de système d’exploitation. Ce didacticiel explique comment créer votre propre image personnalisée d’une machine virtuelle Azure. Vous allez apprendre à effectuer les actions suivantes :

> [!div class="checklist"]
> * Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles
> * Créer une image personnalisée
> * Créer une machine virtuelle à partir d’une image personnalisée
> * La liste de toutes les images hello dans votre abonnement
> * Supprimer une image


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Avant de commencer

étapes Hello ci-dessous décrit en détail comment tootake une machine virtuelle existante et les activer dans personnalisé réutilisable de l’image que vous peuvent utiliser toocreate de nouvelles instances de machine virtuelle.

exemple de hello toocomplete dans ce didacticiel, vous devez disposer d’un ordinateur virtuel existant. Si nécessaire, cet [exemple de script](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) peut en créer une pour vous. Lorsque le travail didacticiel de hello, remplacez machine virtuelle et groupe de ressources hello noms lorsque cela est nécessaire.

## <a name="create-a-custom-image"></a>Créer une image personnalisée

toocreate une image d’un ordinateur virtuel, vous devez tooprepare hello VM par mise hors service, désallouer, puis marque la source de hello machine virtuelle comme généralisé. Une fois hello que machine virtuelle a été préparée, vous pouvez créer une image.

### <a name="deprovision-hello-vm"></a>Annuler le déploiement hello machine virtuelle 

Annulation de généralise hello machine virtuelle en supprimant les informations spécifiques à l’ordinateur. Cette généralisation rend possible toodeploy de machines virtuelles à partir d’une seule image. Au cours de la mise hors service, le nom d’hôte hello est réinitialisé trop*localhost.localdomain*. Les clés d’hôte SSH, les configurations de serveur de noms, le mot de passe racine et les baux DHCP mis en cache sont également supprimés.

toodeprovision hello machine virtuelle, utilisez l’agent de machine virtuelle Azure hello (waagent). l’agent de machine virtuelle Azure Hello est installé sur la machine virtuelle de hello et gère la configuration et l’utilisation de hello contrôleur de structure Azure. Pour plus d’informations, consultez hello [guide de l’utilisateur Linux Agent Azure](agent-user-guide.md).

Se connecter tooyour machine virtuelle à l’aide de SSH et exécution Bonjour commande toodeprovision Bonjour machine virtuelle. Avec hello `+user` argument, dernier compte d’utilisateur configuré hello et toutes les données associées sont également supprimées. Remplacez l’exemple d’adresse IP hello avec hello adresse IP publique de votre machine virtuelle.

SSH toohello machine virtuelle.
```bash
ssh azureuser@52.174.34.95
```
Annuler le déploiement hello machine virtuelle.

```bash
sudo waagent -deprovision+user -force
```
Fermez la session SSH hello.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Désallouer et marquer hello machine virtuelle comme généralisé

toocreate une image, hello machine virtuelle doit toobe désallouée. Désallouer hello machine virtuelle en utilisant [az vm désallouer](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Enfin, définissez état hello Hello machine virtuelle comme généralisée avec [az vm généraliser](/cli//azure/vm#generalize) afin que hello plateforme Azure sache hello machine virtuelle a été généralisé. Vous pouvez uniquement créer une image à partir d’une machine virtuelle généralisée.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Création d’image de hello

Vous pouvez désormais créer une image de machine virtuelle de hello à l’aide de [az image création](/cli//azure/image#create). Hello exemple suivant crée une image nommée *myImage* à partir d’un ordinateur virtuel nommé *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Créer des ordinateurs virtuels à partir de l’image de hello

Maintenant que vous disposez d’une image, vous pouvez créer un ou plusieurs nouveaux ordinateurs virtuels à partir de l’image de hello à l’aide [az vm créer](/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVMfromImage* à partir de l’image hello nommée *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Gestion d’image 

Voici quelques exemples de tâches de gestion d’image courantes et comment toocomplete les à l’aide de hello CLI d’Azure.

Répertoriez toutes les images par nom dans un format de tableau.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Supprimez une image. Cet exemple supprime hello image nommée *myOldImage* de hello *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous montré comment créer une image de machine virtuelle. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Annuler le déploiement de machines virtuelles et généraliser des machines virtuelles
> * Créer une image personnalisée
> * Créer une machine virtuelle à partir d’une image personnalisée
> * La liste de toutes les images hello dans votre abonnement
> * Supprimer une image

Avance toohello toolearn de didacticiel suivant sur les ordinateurs virtuels hautement disponibles.

> [!div class="nextstepaction"]
> [How to use availability sets](tutorial-availability-sets.md) (Comment utiliser des groupes à haute disponibilité).

