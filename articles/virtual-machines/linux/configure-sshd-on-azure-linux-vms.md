---
title: aaaConfigure SSHD sur des Machines virtuelles Azure Linux | Documents Microsoft
description: "Configurer SSHD pour toolockdown SSH tooAzure les ordinateurs virtuels Linux et les meilleures pratiques de sécurité."
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
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a>Configurer SSHD sur des machines virtuelles Linux Azure

Cet article explique comment toolockdown hello serveur SSH sur Linux, tooprovide méthodes recommandées la sécurité et toospeed des processus de connexion SSH hello également à l’aide de clés SSH à la place des mots de passe.  toofurther lockdown SSHD, nous allons utilisateur racine de hello toodisable d’être en mesure de toologin, limiter les utilisateurs hello autorisés toologin via une liste des groupes approuvés, la désactivation de la version 1 du protocole SSH, un bit de clé minimale et configurer avant déconnexion automatique des utilisateurs inactifs.  configuration requise de Hello pour cet article est : un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et [fichiers clés SSH publique et privée](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Commandes rapides

Configurer `/etc/ssh/sshd_config` avec hello suivant les paramètres :

### <a name="disable-password-logins"></a>Désactiver les connexions par mot de passe

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a>Désactiver la connexion à l’utilisateur racine de hello

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a>Liste de groupes autorisés

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a>Liste d’utilisateurs autorisés

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a>Désactiver la version 1 du protocole SSH

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a>Minimum de bits pour les clés

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a>Déconnecter les utilisateurs inactifs

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a>Procédure pas à pas

SSHD est hello serveur SSH qui s’exécute sur hello Linux VM.  SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre MacBook ou votre poste de travail Linux, ou à partir d’un script Bash sur Windows.  SSH est également hello protocole utilisé toosecure et chiffrer la communication hello entre votre station de travail et les hello VM Linux qui SSH effectue également un réseau VPN (Virtual Private Network).

Pour cet article, il est tooyour d’une seule connexion tookeep très important Linux VM ouvrir pour la procédure pas à pas ensemble hello.  Une fois qu’une connexion SSH est établie, il reste comme une session ouverte tant que fenêtre hello n’est pas fermée.  Ayant un terminal connecté, permet de modifications toobe apportée toohello SSHD service sans être verrouillé si une modification avec rupture est effectuée.  Si vous effectuez l’être verrouillés hors de votre VM Linux avec une configuration SSHD rompue, Azure offre une configuration SSHD interrompue avec hello hello capacité tooreset [Extension d’accès Azure VM](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Pour cette raison, nous allons ouvrir deux terminaux et SSH toohello Linux VM à partir des deux d'entre eux.  Nous utiliser hello premier toomake terminal hello modifications tooSSHDs fichier de configuration et redémarrez le service SSHD hello.  Nous utilisons tootest terminal deuxième hello celles modifie une fois le redémarrage du service hello.  Étant donné que nous allons la désactivation des mots de passe SSH et partie de confiance strictement sur les clés SSH, si vos clés SSH ne sont pas corrects et que vous fermez hello connexion toohello machine virtuelle, hello machine virtuelle seront définitivement verrouillé et aucun sera tooit toologin en mesure de rendre obligatoire toobe supprimé et recréé.

## <a name="disable-password-logins"></a>Désactiver les connexions par mot de passe

Hello toosecure de manière plus rapide vous Linux VM est toodisable les connexions de mot de passe.  Lorsque les connexions de mot de passe sont activées, robots web de hello l’analyse démarre immédiatement la tentative de toobrute force mot de passe estimation hello pour votre VM Linux à l’aide de SSH.  Désactive les connexions de mot de passe complètement, permet de hello SSH server tooignore toutes les tentatives de connexion de mot de passe.

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a>Désactiver la connexion à l’utilisateur racine de hello

Suivant les recommandations Linux, hello `root` utilisateur ne doit jamais être connecté à via SSH ou à l’aide de `sudo su`.  Toutes les commandes nécessitant des autorisations au niveau racine doivent toujours être exécutées par le biais hello `sudo` commande, qui enregistre toutes les actions d’audit ultérieur.  Désactivation hello `root` utilisateur de se connecter via une connexion SSH est une étape sécurité meilleures pratiques de qui permet de s’assurer seulement les utilisateurs autorisés peuvent tooSSH.

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a>Liste de groupes autorisés

Le protocole SSH offre une méthode de restriction des utilisateurs et des groupes autorisés à se connecter via SSH.  Cette fonctionnalité utilise des listes tooapprove ou refuser des utilisateurs et groupes spécifiques de se connecter.  Paramètre hello roue groupe toohello `AllowGroups` liste limite les connexions approuvées sur les comptes d’utilisateur SSH toojust qui se trouvent dans le groupe de roulette hello.

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a>Liste d’utilisateurs autorisés

Limiter les utilisateurs toojust de connexions SSH est une façon plus spécifique tooaccomplish hello même tâche que `AllowGroups` est.  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a>Désactiver la version 1 du protocole SSH

La version 1 du protocole SSH n’est pas sécurisée et doit être désactivée.  Version 2 du protocole SSH est la version actuelle hello qui offre un serveur de tooyour de tooSSH de manière sécurisée.  La désactivation de la version 1 de SSH refuse à tous les clients SSH qui tentent de tooestablish une connexion avec le serveur SSH hello à l’aide de la version 1 de SSH.  Seules les connexions SSH version 2 sont autorisées toonegotiate une connexion avec le serveur SSH hello.

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a>Minimum de bits pour les clés

Meilleures pratiques de sécurité, connexions SSH de mot de passe sont désactivées, et seules les clés SSH sont autorisées toobe utilisé tooauthenticate avec serveur SSH de hello.  Ces clés SSH peuvent être créées à l’aide de clés de longueur différente, mesurées en bits.  Meilleures pratiques que les clés de longueur de 2 048 bits sont hello minimale acceptable puissance de la clé des États.  Les clés de moins de 2 048 bits risquent en effet d’être déchiffrées.  Hello du paramètre `ServerKeyBits` trop`2048` autorise toutes les connexions à l’aide de clés de 2 048 bits ou supérieur et refuser les connexions de moins de 2 048 bits.

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a>Déconnecter les utilisateurs inactifs

SSH a hello capacité toodisconnect utilisateurs qui ont des connexions ouvertes qui sont restées inactives au-delà d’une durée de secondes.  Conservation des sessions ouvertes tooonly aux utilisateurs exposition de hello limites active de hello Linux VM.

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a>Redémarrer SSHD

paramètres de hello tooenable dans `/etc/ssh/sshd_config` redémarrer les processus SSHD hello qui redémarre le serveur SSH de hello.  fenêtre de terminal Hello vous utilisez toorestart hello SSH server restent ouverts sans perdre d’ouverture de session SSH hello.  paramètres du serveur SSH nouvelle tootest hello utilisent une deuxième fenêtre de terminal ou un onglet.  À l’aide d’un Bonjour tootest terminal distincte connexion SSH vous permet de toogo précédent et rendre des modifications supplémentaires toohello `/etc/ssh/sshd_config` dans hello premier terminal, sans être verrouillé par une modification avec rupture SSHD.  

### <a name="on-redhat-centos-and-fedora"></a>Sur Redhat, Centos et Fedora

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a>Sur Debian et Ubuntu

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a>Réinitialiser SSHD à l’aide de la commande reset-access Azure

Si vous êtes bloqué d’une configuration de SSHD de toohello de modification avec rupture, vous pouvez utiliser hello extension d’accès Azure VM tooreset hello SSHD configuration arrière toohello configuration d’origine.

Remplacez les exemples de noms par vos propres noms.

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a>Installer Fail2ban

Il est fortement recommandé tooinstall et le programme d’installation open source application hello Fail2ban, les blocs répété tentatives toologin tooyour Linux VM via SSH à l’aide de force brute.  Les journaux de Fail2ban répétées basculé tentatives toologin SSH et crée ensuite des règles de pare-feu tooblock hello l’adresse IP provenant de tentatives de hello.

* [Page d’accueil de Fail2ban](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez configuré et verrouillé de serveur SSH de hello sur votre VM Linux il existe des meilleures pratiques de la sécurité supplémentaire que vous pouvez suivre.  

* [Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [Accès et sécurité dans les modèles Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
