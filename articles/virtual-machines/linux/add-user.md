---
title: aaaAdd un tooa utilisateur VM Linux sur Azure | Documents Microsoft
description: Ajouter un tooa utilisateur Linux VM sur Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Ajouter une machine virtuelle Azure de tooan utilisateur
Une des tâches de premier hello sur n’importe quel VM Linux nouvelle est toocreate un nouvel utilisateur.  Dans cet article, nous Apprenez à créer un compte d’utilisateur sudo, le paramètre hello un mot de passe, ajouter des clés publiques SSH et enfin utiliser `visudo` sudo tooallow sans mot de passe.

Conditions préalables sont : [un compte Azure](https://azure.microsoft.com/pricing/free-trial/), [les clés publiques et privées SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un groupe de ressources Azure hello CLI d’Azure installé et à l’aide de mode de gestionnaire de ressources tooAzure `azure config mode arm`.

## <a name="quick-commands"></a>Commandes rapides
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas
### <a name="introduction"></a>Introduction
L’une des tâches de premier et le plus courant hello avec un nouveau serveur est tooadd un compte d’utilisateur.  Connexions d’accès racine doivent être désactivées et compte de racine de hello lui-même ne doit pas être utilisé avec votre serveur Linux, sudo uniquement.  En donnant une escalade de verrous racine utilisateur des privilèges à l’aide de sudo elle hello tooadminister de manière appropriée et Linux.

À l’aide de la commande hello `useradd` toohello de comptes d’utilisateur Linux VM, nous avons ajouté.  L’exécution de `useradd` modifie `/etc/passwd`, `/etc/shadow`, `/etc/group` et `/etc/gshadow`.  Nous avons ajouté un indicateur de ligne de commande de toohello `useradd` commande tooalso ajouter hello toohello sudo bon groupe d’utilisateurs sur Linux.  Même thou `useradd` crée une entrée dans `/etc/passwd` il ne donne pas nouveau compte d’utilisateur hello un mot de passe.  Nous allons créer un mot de passe initial hello nouvel utilisateur à l’aide de hello simple `passwd` commande.  dernière étape de Hello est toomodify hello sudo règles tooallow qui tooexecute les commandes utilisateur avec des privilèges sudo sans avoir à tooenter un mot de passe pour chaque commande.  Connexion à l’aide de la clé privée de hello présumée ce compte d’utilisateur est protégée contre les mauvais acteurs et allez un accès sudo tooallow sans mot de passe.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Ajout d’un tooan d’utilisateur unique sudo machine virtuelle Azure
Ouvrez une session dans toohello machine virtuelle Azure à l’aide de clés SSH.  Si vous n’avez pas configuré un accès par clé publique SSH, commencez par lire entièrement l’article [Utilisation d’une authentification par clé publique avec Azure](http://link.to/article).  

Hello `useradd` commande termine hello tâches suivantes :

* créer un compte d’utilisateur
* créer un groupe d’utilisateurs avec hello même nom
* Ajouter une entrée vide trop`/etc/passwd`
* Ajouter une entrée vide trop`/etc/gpasswd`

Hello `-G` indicateur de ligne de commande ajoute hello utilisateur compte toohello correcte d’un groupe Linux attribution de privilèges d’escalade de verrous de racine de nouveau compte d’utilisateur hello.

#### <a name="add-hello-user"></a>Ajouter un utilisateur de hello
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Définir le mot de passe
Hello `useradd` commande hello crée et ajoute une entrée tooboth `/etc/passwd` et `/etc/gpasswd` mais ne définit ne pas réellement le mot de passe hello.  Hello mot de passe est ajouté toohello entrée à l’aide de hello `passwd` commande.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Nous disposons désormais d’un utilisateur avec des privilèges sudo sur un serveur de hello.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Ajoutez votre clé publique SSH toohello nouveau compte d’utilisateur
À partir de votre ordinateur, utilisez hello `ssh-copy-id` avec le nouveau mot de passe hello.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Utilisation visudo tooallow sudo sans mot de passe
À l’aide de `visudo` tooedit hello `/etc/sudoers` fichier ajoute plusieurs couches de protection contre la modification incorrecte de ce fichier important.  Lors de l’exécution `visudo`, hello `/etc/sudoers` fichier est verrouillé tooensure aucun autre utilisateur ne peut apporter des modifications pendant qu’il est activement en cours de modification.  Hello `/etc/sudoers` le fichier est extrait également les erreurs par `visudo` lorsque vous essayez de toosave ou se fermer : Impossible d’enregistrer un fichier de programmes sudo rompue.

Nous avons déjà les utilisateurs de groupe par défaut correcte de hello pour un accès sudo.  Nous allons maintenant tooenable ces groupes de sudo toouse sans mot de passe.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Vérifiez les utilisateur hello, ssh clés et sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
