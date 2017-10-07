---
title: "paire de clés aaaDetailed étapes toocreate un SSH pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Découvrez les étapes supplémentaires toocreate une paire de clés SSH publique et privée pour les machines virtuelles Linux dans Azure, ainsi que des certificats spécifiques pour différents cas d’usage."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a>Présentation détaillée toocreate une paire de clés SSH et les certificats supplémentaires pour une Linux VM dans Azure
Avec une paire de clés SSH, vous pouvez créer des Machines virtuelles sur Azure qui par défaut toousing les clés SSH pour l’authentification, hello inutile toolog des mots de passe dans. Les mots de passe peuvent être devinés et ouvrez vos machines virtuelles des toorelentless en force brute tentatives tooguess votre mot de passe. Machines virtuelles créés avec des modèles de CLI d’Azure ou le Gestionnaire de ressources hello peuvent inclure votre clé publique SSH en tant que partie du déploiement hello, vous supprimez une étape de configuration de déploiement post de la désactivation des connexions de mot de passe pour SSH. Cet article fournit des étapes détaillées et des exemples supplémentaires de génération de certificats destinés, par exemple, à être utilisés avec les machines virtuelles Linux. Si vous souhaitez tooquickly créer et utiliser une paire de clés SSH, consultez [la paire de toocreate une clé publique et privée de SSH pour les machines virtuelles dans Azure Linux](mac-create-ssh-keys.md).

## <a name="understanding-ssh-keys"></a>Présentation des clés SSH

À l’aide de clés publiques et privées de SSH est hello toolog de façon plus simple dans tooyour des serveurs Linux. [Chiffrement de clé publique](https://en.wikipedia.org/wiki/Public-key_cryptography) fournit un toolog de façon plus sûre dans tooyour Linux ou VM BSD dans Azure à des mots de passe, qui peuvent être cassée beaucoup plus facilement.

Votre clé publique peut être partagée avec n’importe qui, mais vous seul (ou votre infrastructure de sécurité locale) possédez votre clé privée.  la clé privée SSH Hello doit avoir un [mot de passe sécurisé très](https://www.xkcd.com/936/) (source :[xkcd.com](https://xkcd.com)) toosafeguard il.  Ce mot de passe est simplement tooaccess hello SSH fichier de clé privée et **n’est pas** mot de passe utilisateur hello.  Lorsque vous ajoutez une clé SSH de tooyour mot de passe, elle chiffre la clé privée de hello à l’aide du chiffrement AES 128 bits, de sorte que hello clé privée est inutilisable sans toodecrypt de mot de passe hello il.  Si une personne malveillante a volé votre clé privée et que la clé n’avait pas d’un mot de passe, ils seraient en mesure de toouse privé qui clé toolog serveurs tooany hello de clé publique correspondante.  En revanche, si la clé privée est protégée par un mot de passe, cette dernière ne peut pas être utilisée par l’attaquant. Le mot de passe fournit ainsi une couche supplémentaire de sécurité pour votre infrastructure sur Azure.

Cet article crée une version du protocole SSH 2 paires (également désignée tooas « ssh-rsa » clés), d’un fichier de clé publique et privée RSA qui sont recommandés pour les déploiements avec Azure Resource Manager. *SSH-rsa* clés sont nécessaires sur hello [portal](https://portal.azure.com) pour classique et les déploiements de gestionnaire de ressources.

## <a name="ssh-keys-use-and-benefits"></a>Utilisation et avantages des clés SSH

Azure nécessite au moins 2048 bits, le protocole SSH version 2 RSA format clés publiques et privées ; fichier de clé publique Hello a hello `.pub` format de conteneur. utilisation des clés toocreate hello `ssh-keygen`, ce qui pose une série de questions et puis écrit une clé privée et une clé publique correspondante. Lors de la création d’une machine virtuelle Azure, Azure copies hello toohello de clé publique `~/.ssh/authorized_keys` dossier hello machine virtuelle. Clés SSH dans `~/.ssh/authorized_keys` sont utilisés toochallenge hello client toomatch hello clé privée correspondante sur une connexion SSH.  Lorsqu’une machine virtuelle Linux de Azure est créée à l’aide de clés SSH pour l’authentification, Azure configure hello SSHD server toonot autoriser les connexions de mot de passe, seules les clés SSH.  Par conséquent, en créant les machines virtuelles Azure Linux avec des clés SSH, vous pouvez aider à sécuriser le déploiement des ordinateurs virtuels hello et enregistrer vous-même étape de configuration après le déploiement classique de hello de la désactivation des mots de passe Bonjour **sshd_config** fichier.

## <a name="using-ssh-keygen"></a>Utilisation de ssh-keygen

Cette commande crée un mot de passe sécurisé de paire de clés SSH (chiffré) à l’aide de RSA 2048 bits et il est commenté tooeasily l’identifier.  

SSH clés par défaut sont conservé dans hello `~/.ssh` active.  Si vous n’avez pas un `~/.ssh` répertoire, hello `ssh-keygen` commande crée pour vous par hello autorisations appropriées.

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

*Explication des commandes*

`ssh-keygen`= hello programme utilisé toocreate hello clés

`-t rsa`= type de clé toocreate hello RSA format [wikipedia][parenthèses à fin](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits de clé de hello

`-C "azureuser@myserver"`= un commentaire de fin de toohello ajouté de tooeasily du fichier de clé publique hello identifier.  Normalement, un message électronique est utilisé en tant que commentaire de hello mais vous pouvez utiliser tout ce qui fonctionne le mieux pour votre infrastructure.

## <a name="classic-deploy-using-asm"></a>Déploiement Classic à l’aide de `asm`

Si vous utilisez le modèle de déploiement classique hello (`asm` mode Bonjour CLI), vous pouvez utiliser une clé publique SSH-RSA ou la mise en forme un RFC4716 clé dans un conteneur pem.  clé publique de Hello SSH-RSA est ce qui a été créé précédemment dans cet article à l’aide de `ssh-keygen`.

toocreate un RFC4716 mise en forme de clé à partir d’une clé publique SSH existante :

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a>Exemple de ssh-keygen

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

Fichiers de clés enregistrés :

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

nom de paire de clés Hello pour cet article.  Avoir une paire de clés nommée **id_rsa** est hello par défaut et certains outils peuvent attendre hello **id_rsa** nom de fichier de clé privée comportant une est une bonne idée. répertoire de Hello `~/.ssh/` est l’emplacement par défaut de hello pour les paires de clés SSH et le fichier de configuration SSH hello.  Si non spécifié avec un chemin d’accès complet, `ssh-keygen` crée des clés de hello dans hello répertoire de travail actuel, pas par défaut hello `~/.ssh`.

Une liste de hello `~/.ssh` active.

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

Mot de passe de clé :

`Enter passphrase (empty for no passphrase):`

`ssh-keygen`fait référence tooa le mot de passe pour le fichier de clé privée hello en tant que « une phrase secrète. »  Il s’agit de *fortement* recommandé tooadd une clé privée tooyour de mot de passe. Sans un mot de passe protection hello fichier de clé, toute personne ayant un fichier de hello permet toolog serveur tooany hello la clé publique correspondante. Ajout d’un mot de passe (mot de passe) offre une protection plus au cas où un utilisateur est le fichier clé privée tooyour toogain en mesure de l’accès, vous donné clés de temps toochange hello utilisé tooauthenticate vous.

## <a name="using-ssh-agent-toostore-your-private-key-password"></a>À l’aide de ssh agent toostore votre mot de passe de clé privée

tooavoid taper votre mot de passe du fichier de clé privée avec chaque connexion SSH, vous pouvez utiliser `ssh-agent` toocache votre mot de passe du fichier de clé privée. Si vous utilisez un Mac, hello OSX trousseau stocke en toute sécurité des mots de passe clé privée hello lorsque vous appelez `ssh-agent`.

Vérifiez et utiliser ssh agent, ssh-ajouter tooinform hello SSH système sur les fichiers de clé hello afin que le mot de passe hello n’aurez pas toobe utilisé de manière interactive.

```bash
eval "$(ssh-agent -s)"
```

Maintenant ajouter une clé privée de hello trop`ssh-agent` à l’aide de la commande hello `ssh-add`.

```bash
ssh-add ~/.ssh/id_rsa
```

mot de passe clé privée Hello est maintenant stocké dans `ssh-agent`.

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a>À l’aide de `ssh-copy-id` toocopy hello tooan de clé existant de machine virtuelle
Si vous avez déjà créé une machine virtuelle, vous pouvez installer hello nouvelle SSH publique clé tooyour Linux VM avec :

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a>Créer et configurer un fichier de configuration SSH

Il s’agit d’une meilleure toocreate de pratique recommandée et que vous configurez un `~/.ssh/config` toospeed fichier des ouvertures de session et pour optimiser le comportement de votre client SSH.

Bonjour à l’exemple suivant illustre une configuration standard.

### <a name="create-hello-file"></a>Créer le fichier de hello

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a>Modifiez hello fichier tooadd hello nouvelle configuration SSH :

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a>Exemple de fichier `~/.ssh/config` :

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

Ainsi la configuration SSH vous sections pour chaque serveur tooenable chaque toohave sa propre paire de clés dédié. Hello des paramètres par défaut (`Host *`) sont pour tous les hôtes qui ne correspondent pas à des hôtes spécifiques et hello plus haut dans le fichier de configuration hello.

### <a name="config-file-explained"></a>Explication du fichier de configuration

`Host`= nom hello d’hôte hello soit appelée sur hello Terminal Server.  `ssh fedora22`Indique à `SSH` toouse les valeurs hello dans le bloc de paramètres hello étiqueté `Host fedora22` Remarque : hôte peut être toute étiquette logiques pour votre utilisation et ne représente pas un nom d’hôte réel de hello de n’importe quel serveur.

`Hostname 102.160.203.241`= l’adresse IP de hello ou le nom DNS pour le serveur hello sollicité.

`User ahmet`= toouse de compte d’utilisateur distant hello lors de la connexion toohello server.

`PubKeyAuthentication yes`= Indique SSH vous voulez toouse un toolog clé SSH dans.

`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clé privée SSH hello et toouse de clé publique correspondante pour l’authentification.

## <a name="ssh-into-linux-without-a-password"></a>Connexion SSH sous Linux sans mot de passe

Maintenant que vous avez une paire de clés SSH et un fichier de configuration SSH configuré, vous êtes en mesure de toolog dans tooyour Linux VM rapidement et en toute sécurité. Hello première que connexion de serveur tooa à l’aide d’une invite de commandes hello clé SSH vous pour la phrase secrète de hello pour ce fichier de clé.

```bash
ssh fedora22
```

### <a name="command-explained"></a>Explication des commandes

Lorsque `ssh fedora22` est exécutée SSH tout d’abord localise et charge les paramètres à partir de hello `Host fedora22` bloc, puis charge tous les hello restant des paramètres à partir de hello dernier bloc, `Host *`.

## <a name="next-steps"></a>Étapes suivantes

Ensuite des toocreate les machines virtuelles Azure Linux utilise hello nouveau la clé publique SSH.  Machines virtuelles Azure qui sont créés avec une clé publique SSH en tant que compte de connexion hello sont mieux sécurisées que les machines virtuelles créées avec la méthode de connexion hello par défaut, les mots de passe.  Les machines virtuelles Azure créées à l’aide de clés SSH sont par défaut configurées avec les mots de passe désactivés, bloquant ainsi les tentatives de déchiffrement par force brute.

* [Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Créer une VM Linux sécurisé à l’aide de hello portail Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Créer une VM Linux sécurisé à l’aide de hello CLI d’Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
