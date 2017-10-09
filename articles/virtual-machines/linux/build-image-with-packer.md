---
title: aaaHow toocreate Images de machine virtuelle Azure Linux avec compression | Documents Microsoft
description: "Découvrez comment les images toocreate toouse GARNITURE d’ordinateurs virtuels Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Comment une machine virtuelle Linux toouse GARNITURE toocreate images dans Azure
Chaque ordinateur virtuel (VM) dans Azure est créé à partir d’une image qui définit hello distribution Linux et la version du système d’exploitation. Les images peuvent inclure des configurations et des applications pré-installées. Hello Azure Marketplace fournit des images de premier et le tiers pour distributions courantes et les environnements de l’application, ou vous pouvez créer vos propres besoins de tooyour adaptés des images personnalisées. Cet article décrit en détail comment toouse hello ouvrir outil source [GARNITURE](https://www.packer.io/) toodefine et créer des images personnalisées dans Azure.


## <a name="create-azure-resource-group"></a>Créer un groupe de ressources Azure
Pendant le processus de génération hello, GARNITURE crée des ressources Azure temporaires lorsqu’il crée l’ordinateur virtuel source de hello. toocapture qui de source pour une utilisation en tant qu’image de machine virtuelle, vous devez définir un groupe de ressources. Hello sortie à partir de processus de génération du programme de compression hello est stockée dans ce groupe de ressources.

Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Créer des informations d’identification Azure
Packer s’authentifie auprès d’Azure à l’aide d’un principal de service. Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme Packer. Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure.

Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie GARNITURE doit :

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Voici un exemple de sortie de hello de hello précédant les commandes :

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, vous devez également tooobtain avec l’ID de votre abonnement Azure [afficher de compte az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Vous utilisez la sortie hello à partir de ces deux commandes à l’étape suivante de hello.


## <a name="define-packer-template"></a>Définition du modèle Packer
toobuild images, vous créez un modèle en tant qu’un fichier JSON. Dans le modèle de hello, vous définissez des générateurs et provisioners mener à bien hello réel des processus de génération. Programme de compression a un [un fournisseur pour Azure](https://www.packer.io/docs/builders/azure.html) qui vous permet de toodefine Azure ressources, telles que hello principal des références de service créés dans hello précédant l’étape.

Créez un fichier nommé *ubuntu.json* et coller hello suivant le contenu. Entrez vos propres valeurs pour les éléments suivants de hello :

| Paramètre                           | Où tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Première ligne de la sortie de la commande create `az ad sp` - *appId* |
| *client_secret*                     | Deuxième ligne de la sortie de la commande create `az ad sp` - *password* |
| *tenant_id*                         | Troisième ligne de la sortie de la commande create `az ad sp` - *tenant* |
| *subscription_id*                   | Sortie de la commande `az account show` |
| *managed_image_resource_group_name* | Nom du groupe de ressources que vous avez créé dans la première étape de hello |
| *managed_image_name*                | Nom d’image de disque géré hello qui est créé |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Ce modèle génère une image Ubuntu 16.04 LTS, installe NGINX, puis arrête la machine virtuelle de hello.

> [!NOTE]
> Si vous développez ce informations d’identification d’utilisateur tooprovision de modèle, ajuster la commande d’un fournisseur hello qu’arrête hello agent Azure tooread `-deprovision` plutôt que `deprovision+user`.
> Hello `+user` indicateur supprime tous les comptes d’utilisateur de machine virtuelle de la source hello.


## <a name="build-packer-image"></a>Génération de l’image Packer
Si vous n’avez pas encore installé sur votre ordinateur local, un programme de compression [suivez les instructions d’installation du programme de compression hello](https://www.packer.io/docs/install/index.html).

Créer hello image en spécifiant votre programme de compression des fichiers de modèle comme suit :

```bash
./packer build ubuntu.json
```

Voici un exemple de sortie de hello de hello précédant les commandes :

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Création d’une machine virtuelle à partir d’une image Azure
Vous pouvez à présent créer une machine virtuelle à partir de votre image à l’aide de la commande [az vm create](/cli/azure/vm#create). Spécifiez hello Image que vous avez créé avec hello `--image` paramètre. Hello exemple suivant crée un ordinateur virtuel nommé *myVM* de *myPackerImage* et génère des clés SSH s’ils n’existent pas déjà :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Il prend quelques minutes de toocreate hello machine virtuelle. Une fois que hello machine virtuelle a été créé, prenez note de hello `publicIpAddress` affiché par hello CLI d’Azure. Cette adresse est un site NGINX hello tooaccess utilisées via un navigateur web.

tooallow web tooreach de trafic de votre machine virtuelle, ouvrez port 80 du hello Internet avec [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Test de la machine virtuelle et de NGINX
Vous pouvez désormais ouvrir un navigateur web et entrez `http://publicIpAddress` dans la barre d’adresses hello. Fournissez vos propres adresse IP à partir de la machine virtuelle de hello créer le processus. page NGINX Hello par défaut s’affiche comme dans hello l’exemple suivant :

![Site par défaut NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Étapes suivantes
Dans cet exemple, vous avez utilisé le programme de compression toocreate une image de machine virtuelle avec NGINX déjà installé. Vous pouvez utiliser cette image de machine virtuelle en même temps que les workflows existants de déploiement, telles que toodeploy tooVMs de votre application créé à partir de hello Image avec Ansible, Chef ou Puppet.

Pour obtenir d’autres exemples de modèles Packer pour d’autres distributions Linux, consultez [ce référentiel GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).