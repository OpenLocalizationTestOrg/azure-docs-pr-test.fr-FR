---
title: tooLinux aaaIntroduction dans Azure | Documents Microsoft
description: "Apprenez à utiliser des machines virtuelles Linux sur Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a>TooLinux introduction sur Azure
Cette rubrique fournit une vue d’ensemble de certains aspects de l’utilisation d’ordinateurs virtuels Linux Bonjour cloud Azure. Déploiement d’une machine virtuelle Linux est un processus simple à l’aide d’une image à partir de la galerie de hello.

## <a name="authentication-usernames-passwords-and-ssh-keys"></a>Authentification : noms d’utilisateurs, mots de passe et clés SSH
Lorsque vous créez une machine virtuelle de Linux à l’aide de hello portail Azure, vous êtes invité tooprovide soit un nom d’utilisateur et mot de passe ou une clé publique SSH. choix d’un nom d’utilisateur pour le déploiement d’une machine virtuelle de Linux sur Azure Hello est toohello sujet suivant contrainte : noms des comptes système (UID < 100) déjà présentes dans hello machine virtuelle ne sont pas autorisés, « racine » par exemple.

* Consultez la rubrique [Création d’une machine virtuelle exécutant Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Consultez [comment tooUse SSH avec Linux sur Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="obtaining-superuser-privileges-using-sudo"></a>Obtention de privilèges de superutilisateur avec `sudo`
compte d’utilisateur Hello est spécifié lors du déploiement d’instance de machine virtuelle sur Azure est un compte privilégié. Ce compte est configuré par hello Linux Agent Azure toobe tooelevate en mesure de privilèges tooroot (compte de superutilisateur) à l’aide de hello `sudo` utilitaire. Une fois connecté à l’aide de ce compte d’utilisateur, vous serez en mesure de toorun commandes en tant que racine à l’aide de la syntaxe de la commande hello :

    # sudo <COMMAND>

Vous pouvez éventuellement obtenir un interpréteur de commandes root avec **sudo -s**.

* Consultez la rubrique [Utilisation des privilèges root sur les machines virtuelles Linux dans Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="firewall-configuration"></a>Configuration du pare-feu
Azure fournit un filtre de paquets entrants qui restreint tooports connectivité spécifié dans hello portail Azure. Par défaut, hello uniquement autorisée pour le port est SSH. Vous pouvez ouvrir les ports d’accès tooadditional sur votre machine virtuelle de Linux en configurant des points de terminaison Bonjour portail Azure :

* Voir : [comment tooSet des points de terminaison tooa Machine virtuelle](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

images de Linux Hello Bonjour galerie Azure ne permettent pas de hello *iptables* pare-feu par défaut. Si vous le souhaitez, le pare-feu hello peut être configuré tooprovide un filtrage supplémentaire.

## <a name="hostname-changes"></a>Changements de nom d’hôte
Lorsque vous déployez initialement une instance d’une image Linux, vous êtes tooprovide requis un nom d’hôte pour l’ordinateur virtuel de hello. Une fois que l’ordinateur virtuel de hello est en cours d’exécution, ce nom d’hôte est serveurs DNS de plateforme toohello publié afin que plusieurs machines virtuelles connectées tooeach autres permettre effectuer des recherches d’adresses IP à l’aide des noms d’hôte.

Si les modifications de nom d’hôte sont souhaitées après avoir déployé une machine virtuelle, utilisez commande hello

    # sudo hostname <newname>

Hello Linux Agent Azure inclut une fonctionnalité tooautomatically détecte ce changement de nom correctement configurer hello machine virtuelle toopersist cette modification et ce modifier toohello plateforme DNS les serveurs de publication.

* [Guide d’utilisateur de l’agent Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a>Cloud-Init
Les images **Ubuntu** et **CoreOS** utilisent cloud-init sur Azure, qui fournit des fonctionnalités supplémentaires d’amorçage d’une machine virtuelle.

* [Comment tooInject données personnalisées](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Données personnalisées et Cloud-Init sur Microsoft Azure](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [Création de partitions d’échange Azure à l’aide de Cloud-Init](https://wiki.ubuntu.com/AzureSwapPartitions)
* [Comment tooUse CoreOS sur Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a>Capture d’une image de machine virtuelle
Azure fournit un état de hello toocapture hello capacité d’un ordinateur virtuel existant dans une image qui peut être des instances de machine virtuelle supplémentaire toodeploy utilisé par la suite. Hello Linux Agent Azure peut être utilisé toorollback certaines hello personnalisation effectuée au cours du processus d’approvisionnement de hello. Vous pouvez suivre les étapes de hello ci-dessous toocapture un ordinateur virtuel en tant qu’image :

1. Exécutez **waagent-deprovision** tooundo personnalisation de la configuration. Ou **waagent-deprovision + utilisateur** toooptionally supprimer le compte d’utilisateur hello spécifié lors de la mise en service et toutes les données.
2. Arrêt bas/mise hors tension de l’ordinateur virtuel de hello.
3. Cliquez sur **Capture** Bonjour Azure hello portail ou utilisez PowerShell ou CLI outils toocapture hello virtual machine en tant qu’image.
   
   * Voir : [comment tooCapture un tooUse de Machine virtuelle Linux en tant que modèle](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="attaching-disks"></a>Attachement de disques
Chaque machine virtuelle est associée à un *disque de ressources* local temporaire. Étant donné que les données sur un disque de ressources ne peuvent être durables entre les redémarrages, il est souvent utilisé par les applications et les processus en cours d’exécution dans la machine virtuelle temporaire hello et **temporaire** stockage de données. Il est également utilisé toostore hello des fichiers d’échange pour le système d’exploitation de hello.

Sur Linux, disque de ressources hello est généralement géré par Linux Agent Azure de hello et automatiquement monté trop**/mnt/resource** (ou **/mnt** sur Ubuntu images).

> [!NOTE]
> Notez que le disque ressource hello un **temporaire** sur le disque et peuvent être supprimés et reformaté lorsque hello machine virtuelle est redémarré.
> 
> 

Sur Linux, disque de données hello peut être nommée par noyau hello en tant que `/dev/sdc`, et les utilisateurs doivent toopartition, mettre en forme et de monter cette ressource. Ce sujet est abordé pas à pas dans le didacticiel de hello : [comment tooAttach un tooa de disque de données Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

* **Voir aussi :**[Configuration d’un RAID logiciel sur Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configurer LVM sur une machine virtuelle Linux dans Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

