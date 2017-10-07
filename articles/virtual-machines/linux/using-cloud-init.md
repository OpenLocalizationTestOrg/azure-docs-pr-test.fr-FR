---
title: aaaUse cloud-init toocustomize un VM Linux | Documents Microsoft
description: "Comment toocustomize du cloud-init toouse a Linux VM lors de la création avec hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Utiliser le nuage-init toocustomize un VM Linux lors de la création
Cet article vous explique comment toomake un tooset de script cloud-init hello nom d’hôte, mettre à jour les packages installés et gérer des comptes d’utilisateur avec hello Azure CLI 2.0. scripts d’initialisation de cloud Hello sont appelées lorsque vous créez un ordinateur virtuel (VM) à partir de CLI d’Azure. Pour une présentation plus détaillée de l’installation d’applications, l’écriture de fichiers de configuration et l’injection de clés à partir de Key Vault, consultez [ce didacticiel](tutorial-automate-vm-deployment.md). Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Commandes rapides
Créer un script de init.txt de cloud qui définit le nom d’hôte hello, tous les packages de mises à jour et ajoute un tooLinux d’utilisateur sudo.

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

Créer un toolaunch de groupe de ressources avec des machines virtuelles dans [az groupe créer](/cli/azure/group#create). groupe de ressources hello nommé crée Hello suivant *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage avec hello `--custom-data` paramètre.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas
Lorsque vous lancez une nouvelle machine virtuelle Linux, vous obtenez une machine virtuelle Linux standard, non personnalisée ni adaptée à vos besoins. [Init-cloud](https://cloudinit.readthedocs.org) est un moyen standard de tooinject paramètres de script ou de configuration dans cette VM Linux comme il démarre hello pour la première fois.

Sur Azure, il existe différentes manières de modifications toomake sur un VM Linux qu’il est déployé ou démarré.

* Injectez des scripts à l’aide de cloud-init.
* Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md).
* Un modèle Azure utilisant cloud-init.
* Un modèle Azure utilisant [CustomScriptExtention](extensions-customscript.md).

scripts de tooinject à tout moment après le démarrage :

* Commandes de toorun SSH directement
* Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md), impérative ou dans un modèle Azure
* Des outils de gestion de la configuration tels qu’Ansible, Salt, Chef et Puppet.

> [!NOTE]
> Le VMAccess Extension exécute un script comme racine Bonjour même peut de façon à l’aide de SSH. Toutefois, extension de machine virtuelle hello grâce à plusieurs fonctionnalités que les offres Azure qui peuvent être utile en fonction de votre scénario.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilité de cloud-init lors de la création d’alias d’images de machine virtuelle Azure :
| Alias | Éditeur | Offer | SKU | Version | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |le plus récent |no |
| CoreOS |CoreOS |CoreOS |Stable |le plus récent |yes |
| Debian |credativ |Debian |8 |le plus récent |no |
| openSUSE |SUSE |openSUSE |13.2 |le plus récent |no |
| RHEL |Redhat |RHEL |7,2 |le plus récent |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |le plus récent |yes |

Nous sommes utilisation de nos partenaires tooget cloud-init inclus et utilisation dans des images hello qu’ils fournissent des tooAzure.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Ajouter une création d’ordinateurs virtuels cloud-init script toohello avec hello CLI d’Azure
toolaunch un script d’initialisation de cloud lors de la création d’une machine virtuelle dans Azure, spécifiez le fichier de cloud-init de hello à l’aide de hello CLI d’Azure `--custom-data` basculer.

Créer un toolaunch de groupe de ressources avec des machines virtuelles dans [az groupe créer](/cli/azure/group#create). groupe de ressources hello nommé crée Hello suivant *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Créer un cloud-init script tooset hello nom d’hôte un VM Linux
Un de hello plus simple et des paramètres importants pour n’importe quel VM Linux doit être nom d’hôte hello. Nous pouvons facilement définir ce paramètre en utilisant cloud-init avec ce script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Exemple de script cloud-init nommé `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Au démarrage initial de hello Hello machine virtuelle, ce script cloud-init définit hello hostname trop*MonNomDeServeur*. Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Connexion et vérifiez le nom d’hôte hello Hello nouvelle machine virtuelle.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Création d’un script cloud-init
Pour la sécurité, vous souhaitez que votre tooupdate Ubuntu VM au premier démarrage de hello. À l’aide de cloud-init nous pouvons faire avec hello suivez script, en fonction de distribution de Linux hello que vous utilisez.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Exemple de script cloud-init `cloud_config_apt_upgrade.txt` pour hello Debian famille
```yaml
#cloud-config
apt_upgrade: true
```

Une fois que Linux a démarré, tous les packages hello installé sont mis à jour **apt-get**. Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

Connectez-vous et vérifiez que tous les packages sont mis à jour.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Créer un tooadd de script cloud-init un tooLinux utilisateur
Une des tâches de premier hello sur n’importe quel VM Linux nouvelle est tooadd un utilisateur pour vous-même ou à l’aide de tooavoid *racine*. Clés SSH sont meilleures pratiques pour la sécurité et de facilité d’utilisation et ils sont ajoutés toohello *~/.ssh/authorized_keys* fichier avec ce script init-cloud.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Exemple de script cloud-init `cloud_config_add_users.txt` pour la famille Debian
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Une fois que Linux a démarré, tous les utilisateurs de hello répertorié sont un groupe de sudo toohello créé et ajouté. Créer une VM Linux avec [az vm créer](/cli/azure/vm#create) à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Connexion et vérifier l’utilisateur de hello nouvellement créé.

```bash
ssh myVM
cat /etc/group
```

Sortie

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Étapes suivantes
Init-cloud devient un moyen standard toomodify votre VM Linux au démarrage du système. Azure a également les extensions de machine virtuelle, ce qui vous toomodify votre LinuxVM au démarrage ou pendant son exécution. Par exemple, vous pouvez utiliser hello Azure VMAccessExtension tooreset SSH ou les informations de l’utilisateur pendant l’exécution de hello machine virtuelle. Avec cloud-init, vous aurez besoin d’un mot de passe de redémarrage tooreset hello.

[À propos des extensions et des fonctionnalités des machines virtuelles](extensions-features.md)

[Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension](using-vmaccess-extension.md)
