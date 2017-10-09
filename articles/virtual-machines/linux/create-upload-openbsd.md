---
title: "aaaCreate et télécharger un VM OpenBSD image tooAzure | Documents Microsoft"
description: "Découvrez comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello toocreate du système d’exploitation OpenBSD une machine virtuelle Azure via l’interface CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Créer et télécharger un tooAzure d’image de disque OpenBSD
Cet article vous explique comment toocreate et téléchargez un disque dur virtuel (VHD) qui contient hello système d’exploitation de OpenBSD. Après que l’avoir téléchargée, vous pouvez l’utiliser en tant que vos propres toocreate image un ordinateur virtuel (VM) dans Azure via l’interface CLI d’Azure.


## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez hello éléments suivants :

* **Abonnement Azure** : si vous ne possédez pas de compte, vous pouvez en créer un en quelques minutes. Si vous disposez d’un abonnement MSDN, consultez [Crédit Azure mensuel pour les abonnés Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Dans le cas contraire, découvrez comment trop[créer un compte d’évaluation gratuit](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** -Assurez-vous que vous avez hello dernières [Azure CLI 2.0](/cli/azure/install-azure-cli) installé et connecté tooyour compte Azure avec [ouverture de session az](/cli/azure/#login).
* **Système d’exploitation OpenBSD dans un fichier .vhd** -un système d’exploitation pris en charge OpenBSD (6.1 version) doit être installé tooa un disque dur virtuel. Plusieurs outils existent toocreate les fichiers .vhd. Par exemple, vous pouvez utiliser une solution de virtualisation tels que les fichiers de disque dur virtuel Hyper-V toocreate hello et installer le système d’exploitation de hello. Pour obtenir des instructions sur la façon dont tooinstall et l’utilisation de Hyper-V, consultez [installer Hyper-V et créer une machine virtuelle](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Préparer l’image OpenBSD pour Azure
Sur hello VM où vous avez installé hello OpenBSD système d’exploitation 6.1, qui prend en charge Hyper-V, exécutez hello procédures suivantes :

1. Si DHCP n’est pas activée lors de l’installation, activez le service de hello comme suit :

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Configurez une console série comme suit :

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Configurez l’installation du package comme suit :

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Par défaut, hello `root` utilisateur est désactivé sur les ordinateurs virtuels dans Azure. Les utilisateurs peuvent exécuter des commandes avec des privilèges élevés à l’aide de hello `doas` commande OpenBSD VM. Doas est activé par défaut. Pour plus d’informations, voir [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Installer et configurer les conditions préalables pour hello Azure Agent comme suit :

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. version la plus récente de hello agent Azure Hello se trouvent toujours sur [Github](https://github.com/Azure/WALinuxAgent/releases). Installez l’agent de hello comme suit :

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Après avoir installé l’Agent Azure, il est tooverify une bonne idée qu’elle s’exécute comme suit :
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Annuler le déploiement hello système tooclean et elle est adaptée à la préparation. Hello commande suivante supprime également dernier compte d’utilisateur configuré hello et les données de salutation associée :

    ```sh
    waagent -deprovision+user -force
    ```

Vous pouvez à présent arrêter votre machine virtuelle.


## <a name="prepare-hello-vhd"></a>Préparer hello disque dur virtuel
format VHDX Hello n'est pas pris en charge dans Azure, uniquement **disque dur virtuel fixe**. Vous pouvez convertir le format de disque dur virtuel hello disque toofixed à l’aide du Gestionnaire Hyper-V ou hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) applet de commande. Voici un exemple.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Créer des ressources de stockage et charger
Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload votre disque dur virtuel, créez un compte de stockage avec [créer de compte de stockage az](/cli/azure/storage/account#create). Le nom du compte de stockage devant être unique, entrez votre propre nom. Hello exemple suivant crée un compte de stockage nommé *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol accéder au compte de stockage toohello, d’obtenir la clé de stockage hello avec [liste de clés de compte de stockage az](/cli/azure/storage/account/keys#list) comme suit :

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

hello distinct de toologically disques durs virtuels que vous téléchargez, créer un conteneur dans le compte de stockage hello avec [créer de conteneur de stockage az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Enfin, chargez votre disque dur virtuel avec la commande [az storage blob upload](/cli/azure/storage/blob#upload) comme suit :

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Créer la machine virtuelle à partir de votre disque dur virtuel
Vous pouvez créer une machine virtuelle avec un [exemple de script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) ou directement avec la commande [az vm create](/cli/azure/vm#create). toospecify hello des VHD OpenBSD vous avez téléchargé, utilisez hello `--image` paramètre comme suit :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Obtenir l’adresse IP de hello pour votre VM OpenBSD avec [az vm liste-ip-addresses](/cli/azure/vm#list-ip-addresses) comme suit :

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Vous pouvez désormais SSH tooyour OpenBSD VM normalement :
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez tooknow plus d’informations sur Hyper-V prend en charge sur OpenBSD6.1, lisez [OpenBSD 6.1](https://www.openbsd.org/61.html) et [hyperv.4](http://man.openbsd.org/hyperv.4).

Si vous souhaitez toocreate une machine virtuelle à partir de disque géré, lisez [disque de az](/cli/azure/disk). 
