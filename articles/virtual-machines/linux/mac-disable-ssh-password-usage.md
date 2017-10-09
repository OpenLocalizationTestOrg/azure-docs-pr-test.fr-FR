---
title: les mots de passe SSH aaaDisable sur votre VM Linux en configurant SSHD | Documents Microsoft
description: "Sécurisez votre machine virtuelle Linux sur Azure en désactivant les connexions par mot de passe pour SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a>Désactiver les mots de passe SSH sur votre machine virtuelle Linux en configurant SSHD
Cet article se concentre sur la façon de toolock la sécurité de connexion hello de votre VM Linux.  Dès que hello SSH port 22 est ouvert toohello world robots commencent la tentative de toologin par des mots de passe de déchiffrement.  Cet article décrit comment désactiver les connexions par mot de passe sur SSH.  Attaque par des mots de passe toouse nous protéger hello Linux VM à partir de ce type d’attaque en force supprimant complètement la possibilité de hello.  Hello ajouté bonus est, nous allons configurer SSHD Linux tooonly autoriser les connexions via SSH les clés privés et publics, hello loin tooLinux de toologin de manière plus sécurisée.  les combinaisons possibles Hello de celui-ci nécessiterait la clé privée de tooguess hello est considérable et par conséquent déconseille robots à partir de la même déranger tootry toobrute force SSH clés.

## <a name="goals"></a>Objectifs
* Configurer SSHD toodisallow :
  * Connexions par mot de passe
  * Connexion de l’utilisateur racine
  * Authentification par stimulation/réponse
* Configurer SSHD tooallow :
  * Uniquement les connexions par clés SSH
* Redémarrage de SSHD quand la session est encore ouverte
* Configuration de test hello nouvelle SSHD

## <a name="introduction"></a>Introduction
[Définition de SSH](https://en.wikipedia.org/wiki/Secure_Shell)

SSHD est hello serveur SSH qui s’exécute sur hello Linux VM.  SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre poste de travail MacBook ou Linux.  SSH est également hello protocole utilisé toosecure et chiffrer la communication hello entre votre station de travail et les hello Linux VM.

Pour cet article, il est très important tookeep une connexion tooyour est VM Linux ouvert pour l’ensemble de hello guident.  Pour cette raison, nous allons ouvrir deux terminaux et SSH toohello Linux VM à partir des deux d'entre eux.  Nous utilise hello premier toomake terminal hello modifications tooSSHDs fichier de configuration et redémarrez le service SSHD hello.  Nous allons utiliser hello tootest terminal deuxième celles modifie une fois le redémarrage du service hello.  Étant donné que nous allons la désactivation des mots de passe SSH et partie de confiance strictement sur les clés SSH, si vos clés SSH ne sont pas corrects et que vous fermez hello connexion toohello machine virtuelle, hello machine virtuelle seront définitivement verrouillé et aucun sera tooit toologin en mesure de rendre obligatoire toobe supprimé et recréé.

## <a name="prerequisites"></a>Composants requis
* [Créer des clés SSH sur Linux et Mac pour les machines virtuelles Linux dans Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Compte Azure
  * [Version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)
  * [Portail Azure](http://portal.azure.com)
* Machine virtuelle Linux s’exécutant sur Azure
* Paire de clés publique et privée SSH dans `~/.ssh/`
* Dans la clé publique SSH `~/.ssh/authorized_keys` sur hello Linux VM
* Droits de sudo sur hello machine virtuelle
* Port 22 ouvert

## <a name="quick-commands"></a>Commandes rapides
*Les administrateurs Linux expérimentés souhaitant simplement de la version TLDR hello, commencez ici.  Pour tout le monde afin de pouvoir hello explication détaillée et procédure pas à pas ignorer cette section.*

```bash
sudo vim /etc/ssh/sshd_config
```

Modifiez le fichier de configuration hello comme suit :

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

Redémarrez le service SSHD hello. Sur les distributions basées sur Debian :

```bash
sudo service ssh restart
```

Sur les distributions basées sur Red Hat :

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a>Procédure pas à pas détaillée
Connexion toohello Linux VM sur terminal 1 (T1).  Connexion toohello Linux VM sur 2 terminal (T2).

Dans T2, nous allons fichier de configuration SSHD tooedit hello.  

```bash
sudo vim /etc/ssh/sshd_config
```

À partir d’ici, nous modifier simplement hello paramètres toodisable des mots de passe et activer les connexions de clé SSH.  Il existe de nombreux paramètres dans ce fichier que vous devez rechercher et modifier toomake Linux & SSH aussi sécurisée que nécessaire.

#### <a name="disable-password-logins"></a>Désactiver les connexions par mot de passe

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a>Activer l’authentification par clé publique

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a>Désactiver la connexion racine

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a>Désactiver l’authentification par stimulation/réponse
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a>Redémarrer SSHD
À partir de l’interpréteur de commandes hello T1, vérifiez que vous êtes toujours connecté.  Cela est essentiel pour continuer à avoir accès à votre machine virtuelle si vos clés SSH ne sont pas correctes, car les mots de passe sont désormais désactivés.  Si les paramètres sont incorrects sur votre VM Linux vous pouvez utiliser T1 toofix sshd_config, vous êtes toujours connecté et SSH conservera les connexion hello actif pendant hello les service SSHD redémarrer.

À partir de T2, effectuez l’exécution :

##### <a name="on-hello-debian-family"></a>Sur hello Debian famille
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a>Sur hello RedHat famille
```bash
sudo service sshd restart
```

Les mots de passe sont désormais désactivés sur votre machine virtuelle, ce qui la protège contre les tentatives d’attaque par force brute des connexions par mot de passe.  Avec uniquement SSH clés autorisée, vous serez en mesure de toologin plus rapide et plus sûre.

