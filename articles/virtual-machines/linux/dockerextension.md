---
title: aaaUse hello extension de machine virtuelle de Azure Docker | Documents Microsoft
description: "Découvrez comment toouse hello Docker VM extension tooquickly et en toute sécurité déployer un environnement Docker dans Azure à l’aide de modèles de gestionnaire de ressources et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Créer un environnement de Docker dans Azure à l’aide d’extension de machine virtuelle de Docker hello
Docker est une plate-forme de création d’images qui vous permet de travail tooquickly avec des conteneurs sur Linux et le gestion des conteneurs populaires. Dans Azure, il existe différentes méthodes que vous pouvez déployer selon les besoins de tooyour de Docker. Cet article se concentre sur l’utilisation d’extension de machine virtuelle de Docker hello et modèles Azure Resource Manager par hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Présentation de l’extension Azure Docket VM
Hello extension de machine virtuelle de Azure Docker installe et configure les démon Docker de hello, Docker et du client Docker Compose sur votre ordinateur de virtuel (VM) Linux. Extension de machine virtuelle de Azure Docker hello, vous offre davantage de contrôle et de fonctionnalités que simplement à l’aide d’une Machine Docker ou création de l’hôte de Docker hello vous-même. Ces fonctionnalités, telles que [Docker Compose](https://docs.docker.com/compose/overview/), rendre l’extension de machine virtuelle de Azure Docker hello adaptée pour les environnements de développement ou de production plus fiables.

Pour plus d’informations sur les méthodes de déploiement hello, y compris à l’aide de la Machine Docker et les Services de conteneur Azure, consultez hello suivant des articles :

* prototype de tooquickly une application, vous pouvez créer un seul hôte Docker à l’aide de [Docker ordinateur](docker-machine.md).
* toobuild prêt pour la production d’environnements évolutifs qui fournissent des outils de planification et de gestion supplémentaires, vous pouvez déployer un [Docker Swarm de cluster sur les Services de conteneur Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Déployer un modèle avec hello extension de machine virtuelle de Azure Docker
Nous allons utiliser un existant toocreate de modèle de démarrage rapide un VM Ubuntu qui utilise hello Azure Docker VM extension tooinstall et configurer l’hôte Docker de hello. Vous pouvez afficher le modèle hello ici : [Simple déploiement d’un VM Ubuntu avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

Ensuite, déployez une machine virtuelle avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create) qui inclut l’extension de machine virtuelle de Azure Docker hello de [ce modèle Azure Resource Manager sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Fournissez vos propres valeurs pour *newStorageAccountName*, *adminUsername*, *adminPassword* et *dnsNameForPublicIP* comme suit :

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Il prend quelques minutes pour hello déploiement toofinish. Une fois le déploiement de hello est terminé, [déplacer l’étape de toonext](#deploy-your-first-nginx-container) tooSSH tooyour machine virtuelle. 

Invite de toohello tooinstead redonner le contrôle et de déploiement de hello permettent continuent en arrière-plan de hello, ajoutez éventuellement hello `--no-wait` indicateur toohello précédant la commande. Ce processus vous permet de tooperform autre travail Bonjour CLI pendant le déploiement hello se poursuit pendant quelques minutes. 

Vous pouvez ensuite afficher plus d’informations sur l’état de l’hôte Docker hello avec [afficher de machine virtuelle az](/cli/azure/vm#show). Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Lorsque cette commande retourne *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello VM Bonjour suivant l’étape.

## <a name="deploy-your-first-nginx-container"></a>Déployer votre premier conteneur nginx
tooview les détails de votre machine virtuelle, notamment nom DNS hello, utilisent `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour Docker nouvel hôte à partir de votre ordinateur local comme suit :

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Une fois connecté toohello hôte Docker, nous allons exécuter un conteneur nginx :

```bash
sudo docker run -d -p 80:80 nginx
```

sortie de Hello est similaire toohello exemple suivant comme hello nginx image est téléchargée et un conteneur démarré :

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Vérification du statut de hello de conteneurs hello exécutant sur l’hôte Docker comme suit :

```bash
sudo docker ps
```

sortie de Hello est similaire toohello l’exemple suivant, indiquant que le conteneur de nginx hello est en cours d’exécution et les ports TCP 80 et 443 et transféré :

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

ouverture de votre conteneur dans action, toosee jusqu'à un navigateur web et entrez le nom DNS de hello de l’hôte Docker :

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Référence de modèle pour l’extension Azure Docker VM
Hello l’exemple précédent utilise un modèle de démarrage rapide existant. Vous pouvez également déployer l’extension de machine virtuelle de Azure Docker hello avec vos propres modèles de gestionnaire de ressources. toodo, ajoutez hello suivant tooyour les modèles de gestionnaire de ressources, la définition de hello `vmName` de votre machine virtuelle en conséquence :

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Pour découvrir la procédure pas à pas d’utilisation de modèles Resource Manager, voir la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Étapes suivantes
Vous souhaiterez peut-être trop[configurer le port TCP de hello Docker démon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendre [sécurité de Docker](https://docs.docker.com/engine/security/security/), ou déployer des conteneurs à l’aide de [Docker Compose](https://docs.docker.com/compose/overview/). Pour plus d’informations sur hello Extension de machine virtuelle Docker Azure lui-même, consultez hello [GitHub projet](https://github.com/Azure/azure-docker-extension/).

En savoir plus sur les options de déploiement de Docker supplémentaires hello dans Azure :

* [Utiliser l’ordinateur avec hello pilote Azure Docker](docker-machine.md)  
* [Prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure](docker-compose-quickstart.md).
* [Déploiement d’un cluster Azure Container Service](../../container-service/dcos-swarm/container-service-deployment.md)

