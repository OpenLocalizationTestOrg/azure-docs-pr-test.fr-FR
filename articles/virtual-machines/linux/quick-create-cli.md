---
title: "aaaAzure démarrage rapide - CLI de machine virtuelle créer | Documents Microsoft"
description: "En savoir plus rapidement des machines virtuelles de toocreate avec hello CLI d’Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Créer une machine virtuelle Linux avec hello CLI d’Azure

Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle exécutant Ubuntu server. Une fois que le serveur de hello est déployé, une connexion SSH est créée, et un serveur Web NGINX est installé.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Create virtual machine

Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée un ordinateur virtuel nommé *myVM* et crée des clés SSH s’ils n’existent pas déjà dans un emplacement de la clé par défaut. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant. Prenez note de hello `publicIpAddress`. Cette adresse est utilisée tooaccess hello machine virtuelle.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Ouvrez le port 80 pour le trafic web 

Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure. Si cet ordinateur virtuel est toobe un serveur Web, vous devez tooopen port 80 de hello Internet. Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>Se connecter avec SSH à votre machine virtuelle

La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello. Assurez-vous que tooreplace  *<publicIpAddress>*  avec hello corriger l’adresse IP publique de votre machine virtuelle.  Dans l’exemple ci-dessus, notre adresse IP était *40.68.254.142*.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>Installer NGINX

Suivante de hello utilisez bash sources de package tooupdate de script et installer le dernier package de NGINX hello. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Page d’accueil de vue hello NGINX

Avec NGINX installé et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut NGINX page d’accueil. Être vraiment toouse hello *publicIpAddress* vous documenté au-dessus de la page par défaut toovisit hello. 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Supprimer des ressources

Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web. toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Linux.


> [!div class="nextstepaction"]
> [Didacticiels sur les machines virtuelles Azure Linux](./tutorial-manage-vm.md)
