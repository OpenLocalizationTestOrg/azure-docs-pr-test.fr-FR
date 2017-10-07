---
title: "aaaUse Machine Docker toocreate Linux héberge dans Azure | Documents Microsoft"
description: "Décrit comment toouse Machine Docker toocreate Docker héberge dans Azure."
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
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Comment toouse Machine Docker toocreate héberge dans Azure
Cet article détails comment toouse [Docker ordinateur](https://docs.docker.com/machine/) hôtes toocreate dans Azure. Hello `docker-machine` commande crée une machine virtuelle de Linux (VM) dans Azure, puis installe Docker. Vous pouvez ensuite gérer vos hôtes Docker dans Azure à l’aide hello mêmes outils locaux et les flux de travail.

## <a name="create-vms-with-docker-machine"></a>Créer des machines virtuelles avec Docker Machine
Commencez par obtenir votre ID d’abonnement Azure à l’aide de la commande [az account show](/cli/azure/account#show), comme suit :

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Vous créez des machines virtuelles de hôte Docker dans Azure avec `docker-machine create` en spécifiant *azure* en tant que pilote de hello. Pour plus d’informations, consultez hello [documentation du pilote de Azure Docker](https://docs.docker.com/machine/drivers/azure/)

Hello exemple suivant crée un ordinateur virtuel nommé *myVM*, crée un compte d’utilisateur nommé *azureuser*et ouvre le port *80* sur hello héberger l’ordinateur virtuel. Suivez les toolog invites dans tooyour compte Azure et accorder une Machine Docker autorisations toocreate et gérer les ressources.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

sortie de Hello semble similaire toohello l’exemple suivant :

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
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Configurer votre interpréteur de commandes Docker
hôte de Docker tooconnect tooyour dans Azure, définissez les paramètres de connexion approprié hello. Comme indiqué plus haut fin hello de sortie de hello, affichez les informations de connexion hello pour l’hôte Docker comme suit : 

```bash
docker-machine env myvmdocker
```

Hello la sortie est similaire toohello l’exemple suivant :

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

Vous pouvez soit exécuter hello les paramètres de connexion toodefine hello suggéré commande de configuration (`eval $(docker-machine env myvmdocker)`), ou vous pouvez définir des variables d’environnement hello manuellement. 

## <a name="run-a-container"></a>Exécuter un conteneur
toosee un conteneur en action, vous permet d’exécuter un serveur de Web NGINX base. Créez un conteneur avec `docker run` et exposez le port 80 au trafic web comme suit :

```bash
docker run -d -p 80:80 --restart=always nginx
```

Hello la sortie est similaire toohello l’exemple suivant :

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Affichez les conteneurs en cours d’exécution en utilisant `docker ps`. Hello exemple de sortie suivant affiche hello NGINX conteneur est en cours d’exécution avec le port 80 exposée :

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Conteneur de test hello
Obtenir les adresse IP publique hello de l’hôte Docker comme suit :


```bash
docker-machine ip myvmdocker
```

conteneur de hello toosee dans action, ouvrez un navigateur web et entrez l’adresse IP publique hello noté dans la sortie de hello de hello précédant la commande :

![Exécution d’un conteneur ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez également créer des ordinateurs hôtes avec hello [Extension de machine virtuelle Docker](dockerextension.md). Pour obtenir des exemples sur l’utilisation de Docker Compose, consultez [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples dans Azure](docker-compose-quickstart.md).
