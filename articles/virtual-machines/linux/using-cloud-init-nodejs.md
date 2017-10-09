---
title: "aaaUsing cloud-init toocustomize un VM Linux lors de la création dans Azure | Documents Microsoft"
description: "Comment toocustomize du cloud-init toouse a Linux VM lors de la création avec hello Azure CLI 1.0"
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
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Utiliser le nuage-init toocustomize un VM Linux lors de la création par hello Azure CLI 1.0
Cet article explique comment toomake un tooset de script cloud-init hello nom d’hôte, mettre à jour les packages installés et gérer les comptes d’utilisateur.  scripts de cloud-init Hello sont appelés pendant hello la création d’ordinateurs virtuels à partir de l’interface CLI d’Azure.  article de Hello nécessite :

* un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)).
* Hello [CLI d’Azure](../../cli-install-nodejs.md) connecté `azure login`.
* Hello CLI d’Azure *doit se trouver dans* mode Azure Resource Manager `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="quick-commands"></a>Commandes rapides
Créer un script de init.txt de cloud qui définit le nom d’hôte hello, tous les packages de mises à jour et ajoute un tooLinux d’utilisateur sudo.

```sh
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
Créer des machines virtuelles dans un toolaunch de groupe de ressources.

```azurecli
azure group create myResourceGroup westus
```

Créer une VM Linux à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas
### <a name="introduction"></a>Introduction
Lorsque vous lancez une nouvelle machine virtuelle Linux, vous obtenez une machine virtuelle Linux standard, non personnalisée ni adaptée à vos besoins. [Init-cloud](https://cloudinit.readthedocs.org) est un moyen standard de tooinject paramètres de script ou de configuration dans cette VM Linux comme il démarre hello pour la première fois.

Sur Azure, il existe un trois façons différentes modifications toomake sur un VM Linux qu’il est déployé ou démarré.

* Injectez des scripts à l’aide de cloud-init.
* Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Un modèle Azure utilisant cloud-init.
* Un modèle Azure utilisant [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

scripts de tooinject à tout moment après le démarrage :

* Commandes de toorun SSH directement
* Injection de scripts à l’aide de hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), impérative ou dans un modèle Azure
* Des outils de gestion de la configuration tels qu’Ansible, Salt, Chef et Puppet.

> [!NOTE]
> : L’Extension VMAccess exécute un script comme racine Bonjour même peut de façon à l’aide de SSH.  Toutefois, extension de machine virtuelle hello grâce à plusieurs fonctionnalités que les offres Azure qui peuvent être utile en fonction de votre scénario.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilité de cloud-init lors de la création d’alias d’images de machine virtuelle Azure :
| Alias | Éditeur | Offer | SKU | Version | Cloud-init |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |le plus récent |no |
| CoreOS |CoreOS |CoreOS |Stable |le plus récent |yes |
| Debian |credativ |Debian |8 |le plus récent |no |
| openSUSE |SUSE |openSUSE |13.2 |le plus récent |no |
| RHEL |Redhat |RHEL |7,2 |le plus récent |no |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |le plus récent |yes |

Microsoft est l’utilisation de nos partenaires tooget cloud-init inclus et utilisation dans des images hello qu’ils fournissent des tooAzure.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Ajout d’une création d’ordinateurs virtuels cloud-init script toohello avec hello CLI d’Azure
toolaunch un script d’initialisation de cloud lors de la création d’une machine virtuelle dans Azure, spécifiez le fichier de cloud-init de hello à l’aide de hello CLI d’Azure `--custom-data` basculer.

Créer des machines virtuelles dans un toolaunch de groupe de ressources.

```azurecli
azure group create myResourceGroup westus
```

Créer une VM Linux à l’aide de cloud-init tooconfigure il pendant le démarrage.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Création d’un cloud-init script tooset hello nom d’hôte un VM Linux
Un de hello plus simple et des paramètres importants pour n’importe quel VM Linux doit être nom d’hôte hello. Nous pouvons facilement définir ce paramètre en utilisant cloud-init avec ce script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Exemple de script cloud-init nommé `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Au démarrage initial de hello Hello machine virtuelle, ce script cloud-init définit hello hostname trop`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Connexion et vérifiez le nom d’hôte hello Hello nouvelle machine virtuelle.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Création d’un tooupdate de script cloud-init Linux
Pour la sécurité, vous souhaitez que votre tooupdate Ubuntu VM au premier démarrage de hello.  À l’aide de cloud-init nous pouvons faire avec hello suivez script, en fonction de distribution de Linux hello que vous utilisez.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Exemple de script cloud-init `cloud_config_apt_upgrade.txt` pour hello Debian famille
```sh
#cloud-config
apt_upgrade: true
```

Une fois que Linux a démarré, tous les packages hello installé sont mis à jour `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Création d’un tooadd de script cloud-init un tooLinux utilisateur
Une des tâches de premier hello sur n’importe quel VM Linux nouvelle est tooadd un utilisateur pour vous-même ou à l’aide de tooavoid `root`. Clés SSH sont meilleures pratiques pour la sécurité et de facilité d’utilisation et ils sont ajoutés toohello `~/.ssh/authorized_keys` fichier avec ce script init-cloud.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Exemple de script cloud-init `cloud_config_add_users.txt` pour la famille Debian
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Une fois que Linux a démarré, tous les utilisateurs de hello répertorié sont un groupe de sudo toohello créé et ajouté.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

[À propos des extensions et des fonctionnalités des machines virtuelles](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

