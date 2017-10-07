---
title: aaaCreate une copie de votre VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment toocreate une copie de votre machine virtuelle Azure Linux hello Azure CLI 1.0 dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Créer une copie d’une machine virtuelle de Linux en cours d’exécution sur Azure avec hello Azure CLI 1.0
Cet article vous explique comment une copie de votre machine virtuelle Azure (VM) en cours d’exécution Linux à l’aide de toocreate hello modèle de déploiement de gestionnaire de ressources. Tout d’abord copier sur le système d’exploitation de hello et les données des disques tooa nouveau conteneur, puis configurer les ressources du réseau hello et créer la machine virtuelle hello.

Vous pouvez également [charger et créer une machine virtuelle à partir d’une image de disque personnalisée](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- CLI Azure 1.0 – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="before-you-begin"></a>Avant de commencer
Vérifiez que vous remplissez hello suivant des conditions préalables avant de commencer les étapes hello :

* Vous avez hello [CLI d’Azure](../../cli-install-nodejs.md) téléchargé et installé sur votre ordinateur. 
* Vous devez également recueillir quelques informations concernant votre machine virtuelle Linux Azure existante :

| Informations sur la machine virtuelle source | Où tooget il |
| --- | --- |
| Nom de la machine virtuelle |`azure vm list` |
| Nom du groupe ressources |`azure vm list` |
| Emplacement |`azure vm list` |
| Nom du compte de stockage |`azure storage account list -g <resourceGroup>` |
| Nom du conteneur |`azure storage container list -a <sourcestorageaccountname>` |
| Nom du fichier VHD de la machine virtuelle source |`azure storage blob list --container <containerName>` |

* Vous aurez besoin toomake certains choix sur votre nouvelle machine virtuelle :   <br> -Nom du conteneur    <br> -Nom de la machine virtuelle    <br> -Taille de la machine virtuelle    <br> -Nom du réseau virtuel    <br> -Nom du sous-réseau    <br> -Nom IP    <br> -nom de la carte réseau

## <a name="login-and-set-your-subscription"></a>Se connecter et définir votre abonnement
1. Connexion toohello CLI.

    ```azurecli
    azure login
    ```
2. Assurez-vous que vous êtes en mode Gestionnaire de ressources.

    ```azurecli
    azure config mode arm
    ```
3. Définir l’abonnement approprié de hello. Vous pouvez utiliser « liste des comptes azure » toosee tous vos abonnements.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Arrêter hello machine virtuelle
Arrêt et désallocation de machine virtuelle de la source hello. Vous pouvez utiliser « liste d’ordinateur virtuel Windows azure » tooget une liste de toutes les machines virtuelles de hello dans votre abonnement et de leurs noms de groupe de ressources.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Copiez hello disque dur virtuel
Vous pouvez copier hello disque dur virtuel à partir de la destination de toohello hello source de stockage à l’aide de hello `azure storage blob copy start`. Dans cet exemple, nous allons toocopy hello VHD toohello même compte de stockage, mais un autre conteneur.

conteneur de tooanother toocopy hello VHD Bonjour même compte de stockage, tapez :

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>La configuration du réseau virtuel de hello pour votre nouvelle machine virtuelle
Configurez un réseau virtuel et une carte réseau pour votre nouvelle machine virtuelle. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Créer hello nouvelle machine virtuelle
Vous pouvez maintenant créer une machine virtuelle à partir de votre disque virtuel téléchargé [à l’aide d’un modèle de gestionnaire de ressources](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou via hello CLI en spécifiant hello URI tooyour copié le disque en tapant :

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Étapes suivantes
toolearn comment toouse CLI d’Azure toomanage votre nouvelle machine virtuelle, consultez [les commandes CLI d’Azure pour hello Azure Resource Manager](../azure-cli-arm-commands.md).

