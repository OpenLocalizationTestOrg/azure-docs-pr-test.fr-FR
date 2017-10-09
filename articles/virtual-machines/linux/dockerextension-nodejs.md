---
title: aaaUse hello extension de machine virtuelle de Azure Docker avec hello Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment toouse hello tooquickly d’extension de machine virtuelle de Docker et déployer en toute sécurité un environnement de Docker dans Azure à l’aide de modèles de gestionnaire de ressources."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Créer un environnement de Docker dans Azure à l’aide d’extension de machine virtuelle de Docker hello avec hello Azure CLI 1.0
Docker est une plate-forme de création d’images qui vous permet de travail tooquickly avec des conteneurs sur Linux (et ainsi de Windows) et le gestion des conteneurs populaires. Dans Azure, il existe différentes méthodes que vous pouvez déployer selon les besoins de tooyour de Docker. Cet article se concentre sur l’utilisation d’extension de machine virtuelle de Docker hello et modèles Azure Resource Manager. 

Pour plus d’informations sur les méthodes de déploiement hello, y compris à l’aide de la Machine Docker et les Services de conteneur Azure, consultez hello suivant des articles :

* prototype de tooquickly une application, vous pouvez créer un seul hôte Docker à l’aide de [Docker ordinateur](docker-machine.md).
* Pour les environnements plus grandes et plus stables, vous pouvez utiliser extension de machine virtuelle de Azure Docker hello, qui prend également en charge [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate les déploiements de conteneur cohérent. Cet article explique à l’aide d’extension de machine virtuelle de Azure Docker hello.
* toobuild prêt pour la production d’environnements évolutifs qui fournissent des outils de planification et de gestion supplémentaires, vous pouvez déployer un [Docker Swarm de cluster sur les Services de conteneur Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](dockerextension.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello 

## <a name="azure-docker-vm-extension-overview"></a>Présentation de l’extension Azure Docket VM
Hello extension de machine virtuelle de Azure Docker installe et configure les démon Docker de hello, Docker et du client Docker Compose sur votre ordinateur de virtuel (VM) Linux. Extension de machine virtuelle de Azure Docker hello, vous offre davantage de contrôle et de fonctionnalités que simplement à l’aide d’une Machine Docker ou création de l’hôte de Docker hello vous-même. Ces fonctionnalités, telles que [Docker Compose](https://docs.docker.com/compose/overview/), rendre l’extension de machine virtuelle de Azure Docker hello adaptée pour les environnements de développement ou de production plus fiables.

Les modèles de gestionnaire de ressources Azure définissent hello intégralité de la structure de votre environnement. Les modèles vous toocreate et configurer les ressources, telles que l’hôte Docker de hello machines virtuelles, de stockage, de contrôles d’accès en fonction du rôle (RBAC) et de diagnostics. Vous pouvez réutiliser ces déploiements supplémentaires toocreate de modèles de manière cohérente. Pour plus d’informations sur Azure Resource Manager et les modèles, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Déployer un modèle avec hello extension de machine virtuelle de Azure Docker
Nous allons utiliser un existant toocreate de modèle de démarrage rapide un VM Ubuntu qui utilise hello Azure Docker VM extension tooinstall et configurer l’hôte Docker de hello. Vous pouvez afficher le modèle hello ici : [Simple déploiement d’un VM Ubuntu avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Vous devez hello [dernière CLI d’Azure](../../cli-install-nodejs.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :

```azurecli
azure config mode arm
```

Déployer le modèle hello à l’aide de hello CLI d’Azure, spécifiant hello modèle URI. Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement. Utilisez vos propres nom de groupe de ressources et emplacement comme suit :

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Répondre à votre compte de stockage hello invites tooname, fournir un nom d’utilisateur et un mot de passe et fournissez un nom DNS. Hello la sortie est similaire toohello l’exemple suivant :

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello CLI d’Azure vous renvoie toohello invite après quelques secondes seulement, mais l’hôte Docker est toujours créée et configurée par hello extension de machine virtuelle de Azure Docker. Il prend quelques minutes pour hello déploiement toofinish. Vous pouvez afficher plus d’informations sur l’état de l’hôte Docker hello à l’aide de hello `azure vm show` commande.

Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*. Entrez le nom hello hello du groupe de ressources que vous avez créé dans hello précédant l’étape :

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Hello sortie Hello `azure vm show` commande est similaire toohello l’exemple suivant :

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Début hello de sortie de hello, vous voyez hello **ProvisioningState** Hello machine virtuelle. Lorsque cela affiche *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello machine virtuelle.

Vers la fin de hello de sortie de hello, *nom de domaine complet* affiche le nom de domaine complet de hello de l’hôte Docker. Ce nom de domaine complet est ce que vous utilisez hôte Docker tooSSH tooyour hello restant comme suit.

## <a name="deploy-your-first-nginx-container"></a>Déployer votre premier conteneur nginx
Une fois hello déploiement est terminé, SSH tooyour hôte Docker à partir de votre ordinateur local. Entrez vos propre nom d’utilisateur et nom de domaine complet comme suit :

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
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

ouverture de votre conteneur dans action, toosee jusqu'à un navigateur web et entrez le nom de domaine complet hello de l’hôte Docker :

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Référence de modèle pour l’extension Azure Docker VM
Hello l’exemple précédent utilise un modèle de démarrage rapide existant. Vous pouvez également déployer l’extension de machine virtuelle de Azure Docker hello avec vos propres modèles de gestionnaire de ressources. toodo, ajoutez hello suivant tooyour les modèles de gestionnaire de ressources, la définition de hello *vmName* de votre machine virtuelle en conséquence :

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
    "typeHandlerVersion": "1.1",
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

