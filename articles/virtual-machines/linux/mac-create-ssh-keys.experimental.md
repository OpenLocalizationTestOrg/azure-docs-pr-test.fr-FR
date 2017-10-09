---
title: "paire de clés aaaCreate un SSH pour les machines virtuelles Linux sur Azure | Documents Microsoft"
description: "Créez une paire de clés publique et privée SSH en toute sécurité pour les machines virtuelles Azure Linux."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="2d5e3-103">Créer une paire de clés publique et privée SSH pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="2d5e3-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="2d5e3-104">Cet article vous explique comment toogenerate une protocole version 2 RSA publique et privée clé SSH fichier toouse de paire avec les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="2d5e3-105">Avec une paire de clés SSH, vous pouvez créer des Machines virtuelles sur Azure qui par défaut toousing les clés SSH pour l’authentification, hello inutile toolog des mots de passe dans.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="2d5e3-106">Les mots de passe peuvent être devinés et ouvrez vos machines virtuelles des toorelentless en force brute tentatives tooguess votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="2d5e3-107">Machines virtuelles créées avec les modèles Azure ou hello `azure-cli` peut inclure votre clé publique SSH en tant que partie du déploiement hello, vous supprimez une étape de configuration de déploiement post de la désactivation des connexions de mot de passe pour SSH.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="2d5e3-108">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="2d5e3-108">Quick Commands</span></span>

<span data-ttu-id="2d5e3-109">Exécutez hello en suivant les commandes à partir d’un interpréteur de commandes Bash, en remplaçant les exemples hello avec vos propres choix.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="2d5e3-110">Votre fichier de clé publique SSH est créé par défaut dans `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="2d5e3-111">Lorsque vous êtes invité à l’aide de hello commande suivante, vous devez créer un toosecure « mot de passe » de votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="2d5e3-112">(mot de passe hello est qu'un mot de passe utilisé tooencrypt votre clé privée.)</span><span class="sxs-lookup"><span data-stu-id="2d5e3-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="2d5e3-113">Ajouter la clé de hello nouvellement créé trop`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="2d5e3-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="2d5e3-114">Hello ci-dessus sur les systèmes d’exploitation Linux de presque toutes les distributions de commandes, mais ne fonctionnent pas nécessairement dans des conteneurs, comme environnement de hello peut être contraint radicalement.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="2d5e3-115">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="2d5e3-115">Detailed Walkthrough</span></span>

<span data-ttu-id="2d5e3-116">À l’aide de clés publiques et privées de SSH est hello toolog de façon plus simple dans tooyour des serveurs Linux.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="2d5e3-117">[Chiffrement de clé publique](https://en.wikipedia.org/wiki/Public-key_cryptography) fournit un toolog de façon plus sûre dans tooyour Linux ou VM BSD dans Azure à des mots de passe, qui peuvent être cassée beaucoup plus facilement.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d5e3-118">Votre clé publique peut être partagée avec n’importe qui, mais vous seul (ou votre infrastructure de sécurité locale) possédez votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="2d5e3-119">la clé privée SSH Hello doit avoir un [mot de passe sécurisé très](https://www.xkcd.com/936/) (source :[xkcd.com](https://xkcd.com)) toosafeguard il.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="2d5e3-120">Ce mot de passe est la clé SSH privée tooaccess simplement hello et **n’est pas** mot de passe utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="2d5e3-121">Lorsque vous ajoutez une clé SSH de tooyour mot de passe, elle chiffre la clé privée de hello à l’aide du chiffrement AES 128 bits, de sorte que hello clé privée est inutilisable sans toodecrypt de mot de passe hello il.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="2d5e3-122">Si une personne malveillante a volé votre clé privée et que la clé n’avait pas d’un mot de passe, ils seraient en mesure de toouse privé qui clé toolog serveurs tooany hello de clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="2d5e3-123">En revanche, si la clé privée est protégée par un mot de passe, cette dernière ne peut pas être utilisée par l’attaquant. Le mot de passe fournit ainsi une couche supplémentaire de sécurité pour votre infrastructure sur Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="2d5e3-124">Cet article crée version du protocole SSH 2 RSA publiques et privées fichiers de clés, qui sont recommandés pour les déploiements sur hello Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="2d5e3-125">*SSH-rsa* clés sont nécessaires sur hello [portal](https://portal.azure.com) pour classique et les déploiements de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="2d5e3-126">Désactiver les mots de passe SSH à l’aide des clés SSH</span><span class="sxs-lookup"><span data-stu-id="2d5e3-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="2d5e3-127">Azure requiert des clés publiques et privées d’au moins 2 048 bits au format ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="2d5e3-128">utilisation des clés toocreate hello `ssh-keygen`, ce qui pose une série de questions et puis écrit une clé privée et une clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="2d5e3-129">Lors de la création d’une machine virtuelle Azure, clé publique de hello est copié trop`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="2d5e3-130">Clés SSH dans `~/.ssh/authorized_keys` sont utilisés toochallenge hello client toomatch hello clé privée correspondante sur une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="2d5e3-131">Lorsqu’une machine virtuelle Linux de Azure est créée à l’aide de clés SSH pour l’authentification, Azure configure hello SSHD server toonot autoriser les connexions de mot de passe, seules les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="2d5e3-132">Par conséquent, en créant les machines virtuelles Azure Linux avec des clés SSH, vous pouvez contribuent au déploiement de machine virtuelle hello sécurisé et vous-même enregistrer l’étape de configuration après le déploiement classique de hello de désactivation des mots de passe dans le fichier de configuration sshd_config hello.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="2d5e3-133">Utilisation de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="2d5e3-133">Using ssh-keygen</span></span>

<span data-ttu-id="2d5e3-134">Cette commande crée un mot de passe sécurisé de paire de clés SSH (chiffré) à l’aide de RSA 2048 bits et il est commenté tooeasily l’identifier.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="2d5e3-135">SSH clés par défaut sont conservé dans hello `~/.ssh` active.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="2d5e3-136">Si vous n’avez pas un `~/.ssh` répertoire, hello `ssh-keygen` commande crée pour vous par hello autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="2d5e3-137">*Explication des commandes*</span><span class="sxs-lookup"><span data-stu-id="2d5e3-137">*Command explained*</span></span>

<span data-ttu-id="2d5e3-138">`ssh-keygen`= hello programme utilisé toocreate hello clés</span><span class="sxs-lookup"><span data-stu-id="2d5e3-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="2d5e3-139">`-t rsa`= type de clé toocreate hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="2d5e3-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="2d5e3-140">`-b 2048`= les bits de clé de hello</span><span class="sxs-lookup"><span data-stu-id="2d5e3-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="2d5e3-141">Portail Classic et certificats X.509</span><span class="sxs-lookup"><span data-stu-id="2d5e3-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="2d5e3-142">Si vous utilisez hello Azure [portail classique](https://manage.windowsazure.com/), elle requiert les certificats X.509 pour les clés SSH hello.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="2d5e3-143">Aucun autre type de clé publique SSH n’est autorisé, les certificats X.509 sont *obligatoires*.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="2d5e3-144">toocreate un certificat X.509 à partir de votre clé privée SSH-RSA existante :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="2d5e3-145">Déploiement Classic à l’aide de `asm`</span><span class="sxs-lookup"><span data-stu-id="2d5e3-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="2d5e3-146">Si vous utilisez classique de hello déployer le modèle (gestion des services Azure CLI `asm`), vous pouvez utiliser une clé publique SSH-RSA ou la mise en forme un RFC4716 clé dans un **.pem** conteneur.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="2d5e3-147">clé publique de Hello SSH-RSA est ce qui a été créé précédemment dans cet article à l’aide de `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="2d5e3-148">toocreate un RFC4716 mise en forme de clé à partir d’une clé publique SSH existante :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="2d5e3-149">Exemple de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="2d5e3-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="2d5e3-150">Fichiers de clés enregistrés :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="2d5e3-151">nom de paire de clés Hello pour cet article.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-151">hello key pair name for this article.</span></span>  <span data-ttu-id="2d5e3-152">Avoir une paire de clés nommée **id_rsa** est hello par défaut et certains outils peuvent attendre hello **id_rsa** nom de fichier de clé privée comportant une est une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="2d5e3-153">répertoire de Hello `~/.ssh/` est l’emplacement par défaut de hello pour les paires de clés SSH et le fichier de configuration SSH hello.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="2d5e3-154">Si non spécifié avec un chemin d’accès complet, `ssh-keygen` sera créer des clés de hello dans le répertoire de travail actuel hello, ne Hello pas de valeur par défaut `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="2d5e3-155">Une liste de hello `~/.ssh` active.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="2d5e3-156">Mot de passe de clé :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="2d5e3-157">`ssh-keygen`sous l’appellation tooa mot de passe utilisé tooencrypt hello clé privée « une phrase secrète. »</span><span class="sxs-lookup"><span data-stu-id="2d5e3-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="2d5e3-158">Il s’agit de *fortement* recommandé tooadd une phrase secrète tooyour des paires de clés.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="2d5e3-159">Sans une phrase secrète protection hello clé privée, toute personne ayant un fichier de clé hello permet toolog serveur tooany hello la clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="2d5e3-160">Ajout d’une phrase secrète offre plus de protection au cas où un utilisateur est le fichier clé privée tooyour toogain en mesure de l’accès, de vous donner la clés de temps toochange hello utilisé tooauthenticate vous.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="2d5e3-161">À l’aide de ssh agent toostore votre mot de passe de clé privée</span><span class="sxs-lookup"><span data-stu-id="2d5e3-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="2d5e3-162">mot de passe du fichier tooavoid taper votre clé privée avec chaque connexion SSH, vous pouvez utiliser `ssh-agent` toocache votre mot de passe du fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="2d5e3-163">Si vous utilisez un Mac, hello OSX trousseau stocke en toute sécurité des mots de passe clé privée hello lorsque vous appelez `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="2d5e3-164">Vérifiez et utilisez `ssh-agent` et `ssh-add` tooinform hello SSH système de fichiers de clé hello afin que le mot de passe hello n’aurez pas toobe utilisé de manière interactive.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="2d5e3-165">Maintenant ajouter une clé privée de hello trop`ssh-agent` à l’aide de la commande hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="2d5e3-166">mot de passe clé privée Hello est maintenant stocké dans `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="2d5e3-167">À l’aide de `ssh-copy-id` clé tooinstall hello</span><span class="sxs-lookup"><span data-stu-id="2d5e3-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="2d5e3-168">Si vous avez déjà créé une machine virtuelle, vous pouvez installer hello nouvelle SSH publique clé tooyour Linux VM par hello commande suivante, en remplaçant le nom d’utilisateur de la machine virtuelle hello et l’adresse du serveur hello avec vos propres valeurs :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="2d5e3-169">Créer et configurer un fichier de configuration SSH</span><span class="sxs-lookup"><span data-stu-id="2d5e3-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="2d5e3-170">Il est une meilleure toocreate de pratique et configurer un `~/.ssh/config` toospeed fichier des ouvertures de session et pour optimiser le comportement de votre client SSH.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="2d5e3-171">Bonjour à l’exemple suivant illustre une configuration standard.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="2d5e3-172">Créer le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="2d5e3-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="2d5e3-173">Modifiez hello fichier tooadd hello nouvelle configuration SSH :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="2d5e3-174">Exemple de fichier `~/.ssh/config` :</span><span class="sxs-lookup"><span data-stu-id="2d5e3-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="2d5e3-175">Ainsi la configuration SSH vous sections pour chaque serveur tooenable chaque toohave sa propre paire de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="2d5e3-176">Hello des paramètres par défaut (`Host *`) sont pour tous les hôtes qui ne correspondent pas à des hôtes spécifiques et hello plus haut dans le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="2d5e3-177">Explication du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="2d5e3-177">Config file explained</span></span>

<span data-ttu-id="2d5e3-178">`Host`= nom hello d’hôte hello soit appelée sur hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="2d5e3-179">`ssh fedora22`Indique à `SSH` toouse les valeurs hello dans le bloc de paramètres hello étiqueté `Host fedora22` Remarque : hôte peut être toute étiquette logiques pour votre utilisation et ne représente pas un nom d’hôte réel de hello de n’importe quel serveur.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="2d5e3-180">`Hostname 102.160.203.241`= l’adresse IP de hello ou le nom DNS pour le serveur hello sollicité.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="2d5e3-181">`User ahmet`= toouse de compte d’utilisateur distant hello lors de la connexion toohello server.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="2d5e3-182">`PubKeyAuthentication yes`= Indique SSH vous voulez toouse un toolog clé SSH dans.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="2d5e3-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clé privée SSH hello et toouse de clé publique correspondante pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="2d5e3-184">Connexion SSH sous Linux sans mot de passe</span><span class="sxs-lookup"><span data-stu-id="2d5e3-184">SSH into Linux without a password</span></span>

<span data-ttu-id="2d5e3-185">Maintenant que vous avez une paire de clés SSH et un fichier de configuration SSH configuré, vous êtes en mesure de toolog dans tooyour Linux VM rapidement et en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="2d5e3-186">Hello première que connexion de serveur tooa à l’aide d’une invite de commandes hello clé SSH vous pour la phrase secrète de hello pour ce fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="2d5e3-187">Explication des commandes</span><span class="sxs-lookup"><span data-stu-id="2d5e3-187">Command explained</span></span>

<span data-ttu-id="2d5e3-188">Lorsque `ssh fedora22` est exécutée SSH tout d’abord localise et charge les paramètres à partir de hello `Host fedora22` bloc, puis charge tous les hello restant des paramètres à partir de hello dernier bloc, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d5e3-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d5e3-189">Next Steps</span></span>

<span data-ttu-id="2d5e3-190">Ensuite des toocreate les machines virtuelles Azure Linux utilise hello nouveau la clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="2d5e3-191">Machines virtuelles Azure qui sont créés avec une clé publique SSH en tant que compte de connexion hello sont mieux sécurisées que les machines virtuelles créées avec la méthode de connexion hello par défaut, les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="2d5e3-192">Les machines virtuelles Azure créées à l’aide de clés SSH sont par défaut configurées avec les mots de passe désactivés, bloquant ainsi les tentatives de déchiffrement par force brute.</span><span class="sxs-lookup"><span data-stu-id="2d5e3-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="2d5e3-193">Si vous avez besoin d’assistance pour la création de votre paire de clés SSH ou exiger des certificats supplémentaires, telles que pour les utiliser avec le portail classique de hello, consultez [détaillée des paires de clés SSH toocreate étapes et les certificats](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="2d5e3-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="2d5e3-194">Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="2d5e3-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d5e3-195">Créer une VM Linux sécurisé à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2d5e3-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d5e3-196">Créer une VM Linux sécurisé à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="2d5e3-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
