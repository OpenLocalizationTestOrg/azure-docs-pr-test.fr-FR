---
title: "aaaCreate un VM Linux à l’aide d’un modèle Azure avec Azure CLI 1.0 | Documents Microsoft"
description: "Créer une VM Linux sur Azure à l’aide de hello Azure CLI 1.0 et un modèle Azure Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Comment toocreate un VM Linux à l’aide de hello Azure CLI 1.0 un modèle Azure Resource Manager
Cet article vous explique comment tooquickly déployer un ordinateur virtuel de Linux à l’aide de hello Azure CLI 1.0 et un modèle Azure Resource Manager. article de Hello nécessite :

* un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [Azure CLI 1.0](../../cli-install-nodejs.md) connecté `azure login`.
* Hello CLI d’Azure *doit se trouver dans* mode Azure Resource Manager `azure config mode arm`.

Vous pouvez rapidement déployer un modèle de Linux VM à l’aide de hello [portail Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-command-summary) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="quick-command-summary"></a>Résumé des commandes rapides
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas
Les modèles permettent d’ordinateurs virtuels de toocreate sur Azure avec les paramètres que vous souhaitez toocustomize pendant le lancement de hello, des paramètres tels que les noms d’utilisateur et les noms d’hôte. Pour cet article, nous lançons un modèle Azure utilisant une machine virtuelle Ubuntu ainsi qu’un groupe de sécurité réseau (NSG) avec le port 22 ouvert pour SSH.

Les modèles Azure Resource Manager sont des fichiers JSON qui peuvent être utilisés pour des tâches uniques simples telles que le lancement d’une machine virtuelle Ubuntu tel que réalisé dans cet article.  Modèles Azure peuvent également être utilisé tooconstruct Azure des configurations complexes des environnements entières comme une pile de déploiement de test, de développement ou de production.

## <a name="create-hello-linux-vm"></a>Créer hello Linux VM
Hello suivant exemple de code montre comment toocall `azure group create` toocreate une ressource de groupe et de déployer un VM Linux SSH sécurisé à hello même à l’aide de temps [ce modèle Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). N’oubliez pas que dans votre exemple que vous avez besoin des noms de toouse tooyour unique environnement. Cet exemple utilise *myResourceGroup* en tant que nom de groupe de ressources hello, et *myVM* en tant que nom d’ordinateur virtuel hello.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

sortie de Hello doit ressembler à hello bloc de sortie :

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Cet exemple déployé une machine virtuelle à l’aide de hello `--template-uri` paramètre.  Vous pouvez également télécharger ou créer un modèle localement et passer le modèle hello à l’aide de hello `--template-file` paramètre avec un chemin d’accès de fichier de modèle toohello en tant qu’argument. Hello CLI d’Azure vous invite à entrer les paramètres de hello requis par le modèle de hello.

## <a name="next-steps"></a>Étapes suivantes
Hello de recherche [la galerie de modèles](https://azure.microsoft.com/documentation/templates/) toodiscover le toodeploy d’infrastructures d’application suivant.

