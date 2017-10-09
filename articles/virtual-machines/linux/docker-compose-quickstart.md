---
title: aaaUse Docker Compose sur un VM Linux dans Azure | Documents Microsoft
description: "Comment toouse Docker et composition sur les ordinateurs virtuels Linux avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Obtenir main toodefine Docker et composer et exécuter une application conteneur multiples dans Azure
Avec [composition](http://github.com/docker/compose), vous utilisez une application composée de plusieurs conteneurs Docker un toodefine de fichier texte simple. Vous ensuite lancer votre application dans une commande unique qui fait tout toodeploy votre environnement défini. Par exemple, cet article explique comment tooquickly configurer un blog WordPress avec un service principal de base de données MariaDB SQL sur une VM Ubuntu. Vous pouvez également utiliser tooset composer des applications plus complexes.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Configurer une machine virtuelle Linux en tant qu’hôte Docker
Vous pouvez utiliser différentes procédures Azure et des images disponibles ou des modèles du Gestionnaire de ressources dans Azure Marketplace de hello toocreate un VM Linux et le configurer comme un hôte Docker. Par exemple, consultez [votre environnement à l’aide de hello Extension de machine virtuelle Docker toodeploy](dockerextension.md) tooquickly créer une VM Ubuntu avec hello extension de machine virtuelle de Azure Docker à l’aide un [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Lorsque vous utilisez des extensions de machine virtuelle de Docker hello, votre machine virtuelle est automatiquement configuré comme un hôte Docker et composition est déjà installée.


### <a name="create-docker-host-with-azure-cli-20"></a>Créer un hôte Docker avec Azure CLI 2.0
Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).

Tout d’abord, créez un groupe de ressources pour votre environnement Docker avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement :

```azurecli
az group create --name myResourceGroup --location westus
```

Ensuite, déployez une machine virtuelle avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create) qui inclut l’extension de machine virtuelle de Azure Docker hello de [ce modèle Azure Resource Manager sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Fournissez vos propres valeurs pour *newStorageAccountName*, *adminUsername*, *adminPassword* et *dnsNameForPublicIP* :

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Il prend quelques minutes pour hello déploiement toofinish. Une fois le déploiement de hello est terminé, [déplacer l’étape de toonext](#verify-that-compose-is-installed) tooSSH tooyour machine virtuelle. 

Invite de toohello tooinstead redonner le contrôle et de déploiement de hello permettent continuent en arrière-plan de hello, ajoutez éventuellement hello `--no-wait` indicateur toohello précédant la commande. Ce processus vous permet de tooperform autre travail Bonjour CLI pendant le déploiement hello se poursuit pendant quelques minutes. Vous pouvez ensuite afficher plus d’informations sur l’état de l’hôte Docker hello avec [afficher de machine virtuelle az](/cli/azure/vm#show). Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Lorsque cette commande retourne *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello VM Bonjour suivant l’étape.


## <a name="verify-that-compose-is-installed"></a>Vérifier que Compose est installé
Une fois le déploiement de hello est terminé, SSH tooyour nouvel hôte Docker à l’aide du nom DNS de hello que vous avez fourni pendant le déploiement. Vous pouvez utiliser `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview les détails de votre machine virtuelle, y compris le nom DNS de hello.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck composer est installé sur hello machine virtuelle, exécutez hello de commande suivante :

```bash
docker-compose --version
```

Vous obtenez une sortie similaire*docker-composer 1.6.2, générez 4D 72027*.

> [!TIP]
> Si vous avez utilisé une autre méthode toocreate un hôte Docker et devez tooinstall composer vous-même, consultez hello [composer documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Créer un fichier de configuration docker-compose.yml
Ensuite, créez un `docker-compose.yml` fichier, qui est simplement un fichier texte de configuration, toorun de conteneurs Docker toodefine hello sur hello machine virtuelle. fichier de Hello spécifie hello image toorun sur chaque conteneur (ou elle peut être une build à partir d’un fichier Dockerfile), liens hello entre les conteneurs et les dépendances, les ports et les variables d’environnement nécessaires. Pour plus d’informations sur la syntaxe du fichier yml, consultez [Référence du fichier Compose](https://docs.docker.com/compose/compose-file/).

Créer hello *docker-compose.yml* de fichiers comme suit :

```bash
touch docker-compose.yml
```

Utilisez votre tooadd de l’éditeur de texte favori certains fichiers toohello de données. exemple Hello utilise hello *vi* éditeur :

```bash
vi docker-compose.yml
```

Hello coller l’exemple suivant dans votre fichier texte. Cette configuration utilise des images de hello [docker Hub Registre](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source contenu et création de blogs système de gestion) et un principal lié MariaDB SQL de base de données. Entrez votre propre *MYSQL_ROOT_PASSWORD* comme suit :

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Conteneurs de hello démarrer avec un nouveau message
Dans hello même répertoire que votre *docker-compose.yml* fichier, exécutez hello commande suivante (selon votre environnement, vous devrez peut-être toorun `docker-compose` à l’aide de `sudo`) :

```bash
docker-compose up -d
```

Cette commande démarre les conteneurs Docker hello spécifiés dans *docker-compose.yml*. Il prend une ou deux minutes pour toocomplete de cette étape. Vous consultez toohello similaire de sortie l’exemple suivant :

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Être vraiment toouse hello **-d** option de démarrage afin que les conteneurs hello s’exécutent en arrière-plan de hello en continu.


tooverify qui sont des conteneurs de hello, type `docker-compose ps`. Le résultat suivant doit s’afficher :

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Vous pouvez désormais connecter tooWordPress directement sur la machine virtuelle sur le port 80 de hello. Ouvrez un navigateur web et entrez le nom DNS de hello de votre machine virtuelle (tel que `http://mypublicdns.westus.cloudapp.azure.com`). Vous devez maintenant voir hello que WordPress démarrer écran, où vous effectuez l’installation de hello et prise en main application hello.

![Écran d’accueil WordPress][wordpress_start]

## <a name="next-steps"></a>Étapes suivantes
* Accédez toohello [guide utilisateur de l’extension Docker VM](https://github.com/Azure/azure-docker-extension/blob/master/README.md) pour plus d’options tooconfigure Docker et composition de votre machine virtuelle Docker. Par exemple, une option est tooput hello composition yml fichier (converti tooJSON) directement dans la configuration de hello Hello extension de machine virtuelle de Docker.
* Extraire hello [composer une référence de ligne de commande](http://docs.docker.com/compose/reference/) et [guide de l’utilisateur](http://docs.docker.com/compose/) pour plus d’exemples de génération et de déploiement d’applications de conteneur multiples.
* Utiliser un modèle Azure Resource Manager, soit votre propre ou un obtenue à partir de hello [Communauté](https://azure.microsoft.com/documentation/templates/), toodeploy une machine virtuelle de Azure avec Docker et une application peut être configuré avec la composition. Par exemple, hello [déployer un blog WordPress avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modèle utilise Docker et composition tooquickly déployer WordPress avec un serveur MySQL principal sur un VM Ubuntu.
* Essayez d’intégrer Docker Compose à un cluster Docker Swarm. Pour examiner des scénarios, consultez [Utilisation de Compose avec Swarm](https://docs.docker.com/compose/swarm/) .

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
