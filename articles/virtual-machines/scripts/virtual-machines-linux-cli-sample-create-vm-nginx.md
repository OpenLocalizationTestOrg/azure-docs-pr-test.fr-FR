---
title: "aaaAzure exemple de Script CLI - créer un VM Linux avec NGINX | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a>Créer une machine virtuelle avec NGINX

Ce script crée une Machine virtuelle Azure et utilise l’Extension de Script personnalisé Machine virtuelle Azure de hello tooinstall NGINX. Après avoir exécuté le script de hello, vous pouvez accéder à un site Web de démonstration sur hello adresse IP publique de machine virtuelle de hello.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Exemple de script

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a>Extension de script personnalisé

extension de script personnalisé Hello copie ce script sur l’ordinateur virtuel de hello. script de Hello est alors exécutée tooinstall et configurer un serveur de web NGINX. 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a>Nettoyer le déploiement 

Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [az vm create](https://docs.microsoft.com/cli/azure/vm#create) | Crée un ordinateur virtuel de hello. Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.  |
| [az vm open-port](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant. Dans cet exemple, le port 80 est ouvert pour le trafic HTTP. |
| [azure vm extension set](https://docs.microsoft.com/cli/azure/vm/extension#set) | Ajoute et exécute un tooa d’extension de machine virtuelle machine virtuelle. Dans cet exemple, extension de script personnalisé hello est utilisé tooinstall NGINX.|
| [az group delete](https://docs.microsoft.com/cli/azure/vm/extension#set) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).

Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
