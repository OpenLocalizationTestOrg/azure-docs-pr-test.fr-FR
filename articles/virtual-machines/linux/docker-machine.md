---
title: "Utiliser Docker Machine pour créer des hôtes Linux dans Azure | Microsoft Docs"
description: "Décrit l’utilisation de Docker Machine pour créer des hôtes Docker dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a>Comment utiliser Docker Machine pour créer des hôtes dans Azure
Cet article explique comment utiliser [Docker Machine](https://docs.docker.com/machine/) pour créer des hôtes dans Azure. La commande `docker-machine` crée une machine virtuelle Linux dans Azure, puis installe Docker. Vous pouvez ensuite gérer vos hôtes Docker dans Azure en utilisant les mêmes outils et flux de travail locaux.

## <a name="create-vms-with-docker-machine"></a>Créer des machines virtuelles avec Docker Machine
Commencez par obtenir votre ID d’abonnement Azure à l’aide de la commande [az account show](/cli/azure/account#show), comme suit :

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Vous créez des machines virtuelles hôtes Docker dans Azure avec `docker-machine create` en spécifiant *azure* comme pilote. Consultez la [Documentation Docker Azure pilote](https://docs.docker.com/machine/drivers/azure/) pour plus d’informations.

L’exemple suivant crée une machine virtuelle nommée *myVM*, crée un compte d’utilisateur nommé *azureuser*, puis ouvre le port *80* sur la machine virtuelle hôte. Suivez les invites pour vous connecter à votre compte Azure et accorder à Docker Machine les autorisations nécessaires pour créer et gérer des ressources.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

Le résultat ressemble à l’exemple qui suit :

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Configurer votre interpréteur de commandes Docker
Pour vous connecter à votre hôte Docker dans Azure, définissez les paramètres de connexion appropriés. Entrez la commande suivante pour afficher les informations de connexion pour votre hôte Docker, comme indiqué à la fin de la sortie : 

```bash
docker-machine env myvmdocker
```

Le résultat ressemble à l’exemple suivant :

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

Pour définir les paramètres de connexion, vous pouvez exécuter la commande de configuration suggérée (`eval $(docker-machine env myvmdocker)`) ou définir les variables d’environnement manuellement. 

## <a name="run-a-container"></a>Exécuter un conteneur
Pour voir un conteneur en action, vous pouvez exécuter un serveur web NGINX de base. Créez un conteneur avec `docker run` et exposez le port 80 au trafic web comme suit :

```bash
docker run -d -p 80:80 --restart=always nginx
```

Le résultat ressemble à l’exemple suivant :

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Affichez les conteneurs en cours d’exécution en utilisant `docker ps`. L’exemple de sortie suivant montre le conteneur NGINX en cours d’exécution avec le port 80 exposé :

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a>Tester le conteneur
Procédez comme suit pour obtenir l’adresse IP publique de l’hôte Docker :


```bash
docker-machine ip myvmdocker
```

Pour voir le conteneur en action, ouvrez un navigateur web et entrez l’adresse IP publique notée dans la sortie de la commande précédente :

![Exécution d’un conteneur ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez également créer des hôtes avec [l’extension de machine virtuelle Docker](dockerextension.md). Pour obtenir des exemples sur l’utilisation de Docker Compose, consultez [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples dans Azure](docker-compose-quickstart.md).
