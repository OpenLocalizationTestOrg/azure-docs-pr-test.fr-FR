---
title: "aaaDifferent manières toocreate un VM Linux dans Azure | Microsoft Azure"
description: "Découvrez les différentes façons de hello toocreate une machine virtuelle de Linux sur Azure, y compris des liens tootools et des didacticiels pour chaque méthode."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Différentes façons toocreate un VM Linux
Vous avez une grande souplesse hello dans Azure toocreate un ordinateur de virtuel (VM) Linux à l’aide des outils et des flux de travail tooyou à l’aise. Cet article résume ces différences et des exemples pour la création de vos machines virtuelles Linux, y compris hello Azure CLI 2.0. Vous pouvez également afficher les choix de la création, y compris hello [Azure CLI 1.0](creation-choices-nodejs.md).

Hello [Azure CLI 2.0](/cli/azure/install-az-cli2) n’est disponible sur plusieurs plateformes via un package npm, les packages de distribution fournie ou conteneur Docker. Installez hello build la plus appropriée pour votre environnement et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login)

* [Créer une VM Linux avec hello Azure CLI 2.0](quick-create-cli.md)
  
  * Avec la commande [az group create](/cli/azure/group#create), créez un groupe de ressources nommé *myResourceGroup* : 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Créer une machine virtuelle avec [az vm créer](/cli/azure/vm#create) nommé *myVM* à l’aide de hello dernières *UbuntuLTS* de l’image et générer des clés SSH s’ils n’existent pas déjà dans *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Créer une machine virtuelle Linux à l’aide d’un modèle Azure](create-ssh-secured-vm-from-template.md)
  
  * Hello exemple suivant utilise [créer de déploiement de groupe az](/cli/azure/group/deployment#create) toocreate une machine virtuelle à partir d’un modèle stocké sur GitHub :
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Créer une machine virtuelle Linux et personnaliser avec cloud-init](tutorial-automate-vm-deployment.md)

* [Créer une application hautement disponible et à charge équilibrée sur plusieurs machines virtuelles Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Portail Azure
Hello [portail Azure](https://portal.azure.com) vous permet de tooquickly créer une machine virtuelle, car il n’y a rien tooinstall sur votre système. Bonjour Azure toocreate portail Bonjour machine virtuelle, utilisez :

* [Créer une VM Linux à l’aide de hello portail Azure](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Système d'exploitation et choix d'images
Lorsque vous créez une machine virtuelle, vous choisissez une image basée sur hello souhaité toorun de système d’exploitation. Microsoft Azure et ses partenaires proposent de nombreuses images, dont certaines comprennent des applications et des outils préinstallés. Ou téléchargez un de vos propres images (consultez [hello suivant la section](#use-your-own-image)).

### <a name="azure-images"></a>Images Microsoft Azure
Hello d’utilisation [image de machine virtuelle az](/cli/azure/vm/image) commandes toosee ce qui est disponible par le serveur de publication, publication de distribution et aux builds.

Répertorier les éditeurs disponibles :

```azurecli
az vm image list-publishers --location eastus
```

Répertorier les produits disponibles (offres) pour un éditeur donné :

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Répertorier les références disponibles (versions distributeur) d’une offre donnée :

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Répertorier toutes les images disponibles pour une version donnée :

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Pour plus d’exemples sur l’exploration et à l’aide des images disponibles, consultez [naviguer et sélectionnez les images de machine virtuelle Azure avec hello CLI d’Azure](cli-ps-findimage.md).

Hello [az vm créer](/cli/azure/vm#create) commande a l’alias que vous pouvez utiliser l’accès tooquickly hello des versions plus courantes et leurs dernières versions. L’alias est souvent plus rapide que la spécification de serveur de publication hello, offre, référence (SKU) et la version chaque fois que vous créez une machine virtuelle :

| Alias | Éditeur | Offer | SKU | Version |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |le plus récent |
| CoreOS |CoreOS |CoreOS |Stable |le plus récent |
| Debian |credativ |Debian |8 |le plus récent |
| openSUSE |SUSE |openSUSE |13.2 |le plus récent |
| RHEL |Redhat |RHEL |7,2 |le plus récent |
| SLES |SLES |SLES |12-SP1 |le plus récent |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |le plus récent |

### <a name="use-your-own-image"></a>Utiliser votre propre image
Si vous avez besoin de personnalisations spécifiques, vous pouvez utiliser une image basée sur une machine virtuelle Azure existante, en capturant cette machine virtuelle. Vous pouvez également télécharger une image créée sur site. Pour plus d’informations sur les versions prises en charge et toouse vos propres images, voir hello suivants articles :

* [Distributions prises en charge par Azure](endorsed-distros.md)
* [Informations concernant les distributions non approuvées](create-upload-generic.md)
* [Comment toocreate une image à partir d’une machine virtuelle Azure existante](tutorial-custom-images.md).
  
  * Exemple de démarrage rapide des commandes toocreate une image à partir d’une machine virtuelle Azure existante :
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Étapes suivantes
* Créer une VM Linux avec hello [CLI](quick-create-cli.md), à partir de hello [portal](quick-create-portal.md), ou en utilisant un [modèle Azure Resource Manager](../windows/cli-deploy-templates.md).
* Après avoir créé une machine virtuelle Linux, [en savoir plus sur les disques et les stockages Azure](tutorial-manage-disks.md).
* Les étapes trop rapide[réinitialiser un mot de passe ou des clés SSH et gérer des utilisateurs](using-vmaccess-extension.md).
