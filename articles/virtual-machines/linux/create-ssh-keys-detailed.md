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
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="73f0f-103">Présentation détaillée toocreate une paire de clés SSH et les certificats supplémentaires pour une Linux VM dans Azure</span><span class="sxs-lookup"><span data-stu-id="73f0f-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="73f0f-104">Avec une paire de clés SSH, vous pouvez créer des Machines virtuelles sur Azure qui par défaut toousing les clés SSH pour l’authentification, hello inutile toolog des mots de passe dans.</span><span class="sxs-lookup"><span data-stu-id="73f0f-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="73f0f-105">Les mots de passe peuvent être devinés et ouvrez vos machines virtuelles des toorelentless en force brute tentatives tooguess votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="73f0f-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="73f0f-106">Machines virtuelles créés avec des modèles de CLI d’Azure ou le Gestionnaire de ressources hello peuvent inclure votre clé publique SSH en tant que partie du déploiement hello, vous supprimez une étape de configuration de déploiement post de la désactivation des connexions de mot de passe pour SSH.</span><span class="sxs-lookup"><span data-stu-id="73f0f-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="73f0f-107">Cet article fournit des étapes détaillées et des exemples supplémentaires de génération de certificats destinés, par exemple, à être utilisés avec les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="73f0f-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="73f0f-108">Si vous souhaitez tooquickly créer et utiliser une paire de clés SSH, consultez [la paire de toocreate une clé publique et privée de SSH pour les machines virtuelles dans Azure Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="73f0f-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="73f0f-109">Présentation des clés SSH</span><span class="sxs-lookup"><span data-stu-id="73f0f-109">Understanding SSH keys</span></span>

<span data-ttu-id="73f0f-110">À l’aide de clés publiques et privées de SSH est hello toolog de façon plus simple dans tooyour des serveurs Linux.</span><span class="sxs-lookup"><span data-stu-id="73f0f-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="73f0f-111">[Chiffrement de clé publique](https://en.wikipedia.org/wiki/Public-key_cryptography) fournit un toolog de façon plus sûre dans tooyour Linux ou VM BSD dans Azure à des mots de passe, qui peuvent être cassée beaucoup plus facilement.</span><span class="sxs-lookup"><span data-stu-id="73f0f-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="73f0f-112">Votre clé publique peut être partagée avec n’importe qui, mais vous seul (ou votre infrastructure de sécurité locale) possédez votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="73f0f-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="73f0f-113">la clé privée SSH Hello doit avoir un [mot de passe sécurisé très](https://www.xkcd.com/936/) (source :[xkcd.com](https://xkcd.com)) toosafeguard il.</span><span class="sxs-lookup"><span data-stu-id="73f0f-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="73f0f-114">Ce mot de passe est simplement tooaccess hello SSH fichier de clé privée et **n’est pas** mot de passe utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="73f0f-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="73f0f-115">Lorsque vous ajoutez une clé SSH de tooyour mot de passe, elle chiffre la clé privée de hello à l’aide du chiffrement AES 128 bits, de sorte que hello clé privée est inutilisable sans toodecrypt de mot de passe hello il.</span><span class="sxs-lookup"><span data-stu-id="73f0f-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="73f0f-116">Si une personne malveillante a volé votre clé privée et que la clé n’avait pas d’un mot de passe, ils seraient en mesure de toouse privé qui clé toolog serveurs tooany hello de clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="73f0f-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="73f0f-117">En revanche, si la clé privée est protégée par un mot de passe, cette dernière ne peut pas être utilisée par l’attaquant. Le mot de passe fournit ainsi une couche supplémentaire de sécurité pour votre infrastructure sur Azure.</span><span class="sxs-lookup"><span data-stu-id="73f0f-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="73f0f-118">Cet article crée une version du protocole SSH 2 paires (également désignée tooas « ssh-rsa » clés), d’un fichier de clé publique et privée RSA qui sont recommandés pour les déploiements avec Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73f0f-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="73f0f-119">*SSH-rsa* clés sont nécessaires sur hello [portal](https://portal.azure.com) pour classique et les déploiements de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="73f0f-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="73f0f-120">Utilisation et avantages des clés SSH</span><span class="sxs-lookup"><span data-stu-id="73f0f-120">SSH keys use and benefits</span></span>

<span data-ttu-id="73f0f-121">Azure nécessite au moins 2048 bits, le protocole SSH version 2 RSA format clés publiques et privées ; fichier de clé publique Hello a hello `.pub` format de conteneur.</span><span class="sxs-lookup"><span data-stu-id="73f0f-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="73f0f-122">utilisation des clés toocreate hello `ssh-keygen`, ce qui pose une série de questions et puis écrit une clé privée et une clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="73f0f-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="73f0f-123">Lors de la création d’une machine virtuelle Azure, Azure copies hello toohello de clé publique `~/.ssh/authorized_keys` dossier hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="73f0f-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="73f0f-124">Clés SSH dans `~/.ssh/authorized_keys` sont utilisés toochallenge hello client toomatch hello clé privée correspondante sur une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="73f0f-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="73f0f-125">Lorsqu’une machine virtuelle Linux de Azure est créée à l’aide de clés SSH pour l’authentification, Azure configure hello SSHD server toonot autoriser les connexions de mot de passe, seules les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="73f0f-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="73f0f-126">Par conséquent, en créant les machines virtuelles Azure Linux avec des clés SSH, vous pouvez aider à sécuriser le déploiement des ordinateurs virtuels hello et enregistrer vous-même étape de configuration après le déploiement classique de hello de la désactivation des mots de passe Bonjour **sshd_config** fichier.</span><span class="sxs-lookup"><span data-stu-id="73f0f-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="73f0f-127">Utilisation de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="73f0f-127">Using ssh-keygen</span></span>

<span data-ttu-id="73f0f-128">Cette commande crée un mot de passe sécurisé de paire de clés SSH (chiffré) à l’aide de RSA 2048 bits et il est commenté tooeasily l’identifier.</span><span class="sxs-lookup"><span data-stu-id="73f0f-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="73f0f-129">SSH clés par défaut sont conservé dans hello `~/.ssh` active.</span><span class="sxs-lookup"><span data-stu-id="73f0f-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="73f0f-130">Si vous n’avez pas un `~/.ssh` répertoire, hello `ssh-keygen` commande crée pour vous par hello autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="73f0f-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="73f0f-131">*Explication des commandes*</span><span class="sxs-lookup"><span data-stu-id="73f0f-131">*Command explained*</span></span>

<span data-ttu-id="73f0f-132">`ssh-keygen`= hello programme utilisé toocreate hello clés</span><span class="sxs-lookup"><span data-stu-id="73f0f-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="73f0f-133">`-t rsa`= type de clé toocreate hello RSA format [wikipedia][parenthèses à fin](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits de clé de hello</span><span class="sxs-lookup"><span data-stu-id="73f0f-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="73f0f-134">`-C "azureuser@myserver"`= un commentaire de fin de toohello ajouté de tooeasily du fichier de clé publique hello identifier.</span><span class="sxs-lookup"><span data-stu-id="73f0f-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="73f0f-135">Normalement, un message électronique est utilisé en tant que commentaire de hello mais vous pouvez utiliser tout ce qui fonctionne le mieux pour votre infrastructure.</span><span class="sxs-lookup"><span data-stu-id="73f0f-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="73f0f-136">Déploiement Classic à l’aide de `asm`</span><span class="sxs-lookup"><span data-stu-id="73f0f-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="73f0f-137">Si vous utilisez le modèle de déploiement classique hello (`asm` mode Bonjour CLI), vous pouvez utiliser une clé publique SSH-RSA ou la mise en forme un RFC4716 clé dans un conteneur pem.</span><span class="sxs-lookup"><span data-stu-id="73f0f-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="73f0f-138">clé publique de Hello SSH-RSA est ce qui a été créé précédemment dans cet article à l’aide de `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="73f0f-139">toocreate un RFC4716 mise en forme de clé à partir d’une clé publique SSH existante :</span><span class="sxs-lookup"><span data-stu-id="73f0f-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="73f0f-140">Exemple de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="73f0f-140">Example of ssh-keygen</span></span>

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

<span data-ttu-id="73f0f-141">Fichiers de clés enregistrés :</span><span class="sxs-lookup"><span data-stu-id="73f0f-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="73f0f-142">nom de paire de clés Hello pour cet article.</span><span class="sxs-lookup"><span data-stu-id="73f0f-142">hello key pair name for this article.</span></span>  <span data-ttu-id="73f0f-143">Avoir une paire de clés nommée **id_rsa** est hello par défaut et certains outils peuvent attendre hello **id_rsa** nom de fichier de clé privée comportant une est une bonne idée.</span><span class="sxs-lookup"><span data-stu-id="73f0f-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="73f0f-144">répertoire de Hello `~/.ssh/` est l’emplacement par défaut de hello pour les paires de clés SSH et le fichier de configuration SSH hello.</span><span class="sxs-lookup"><span data-stu-id="73f0f-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="73f0f-145">Si non spécifié avec un chemin d’accès complet, `ssh-keygen` crée des clés de hello dans hello répertoire de travail actuel, pas par défaut hello `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="73f0f-146">Une liste de hello `~/.ssh` active.</span><span class="sxs-lookup"><span data-stu-id="73f0f-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="73f0f-147">Mot de passe de clé :</span><span class="sxs-lookup"><span data-stu-id="73f0f-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="73f0f-148">`ssh-keygen`fait référence tooa le mot de passe pour le fichier de clé privée hello en tant que « une phrase secrète. »</span><span class="sxs-lookup"><span data-stu-id="73f0f-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="73f0f-149">Il s’agit de *fortement* recommandé tooadd une clé privée tooyour de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="73f0f-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="73f0f-150">Sans un mot de passe protection hello fichier de clé, toute personne ayant un fichier de hello permet toolog serveur tooany hello la clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="73f0f-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="73f0f-151">Ajout d’un mot de passe (mot de passe) offre une protection plus au cas où un utilisateur est le fichier clé privée tooyour toogain en mesure de l’accès, vous donné clés de temps toochange hello utilisé tooauthenticate vous.</span><span class="sxs-lookup"><span data-stu-id="73f0f-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="73f0f-152">À l’aide de ssh agent toostore votre mot de passe de clé privée</span><span class="sxs-lookup"><span data-stu-id="73f0f-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="73f0f-153">tooavoid taper votre mot de passe du fichier de clé privée avec chaque connexion SSH, vous pouvez utiliser `ssh-agent` toocache votre mot de passe du fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="73f0f-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="73f0f-154">Si vous utilisez un Mac, hello OSX trousseau stocke en toute sécurité des mots de passe clé privée hello lorsque vous appelez `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="73f0f-155">Vérifiez et utiliser ssh agent, ssh-ajouter tooinform hello SSH système sur les fichiers de clé hello afin que le mot de passe hello n’aurez pas toobe utilisé de manière interactive.</span><span class="sxs-lookup"><span data-stu-id="73f0f-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="73f0f-156">Maintenant ajouter une clé privée de hello trop`ssh-agent` à l’aide de la commande hello `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="73f0f-157">mot de passe clé privée Hello est maintenant stocké dans `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="73f0f-158">À l’aide de `ssh-copy-id` toocopy hello tooan de clé existant de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="73f0f-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="73f0f-159">Si vous avez déjà créé une machine virtuelle, vous pouvez installer hello nouvelle SSH publique clé tooyour Linux VM avec :</span><span class="sxs-lookup"><span data-stu-id="73f0f-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="73f0f-160">Créer et configurer un fichier de configuration SSH</span><span class="sxs-lookup"><span data-stu-id="73f0f-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="73f0f-161">Il s’agit d’une meilleure toocreate de pratique recommandée et que vous configurez un `~/.ssh/config` toospeed fichier des ouvertures de session et pour optimiser le comportement de votre client SSH.</span><span class="sxs-lookup"><span data-stu-id="73f0f-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="73f0f-162">Bonjour à l’exemple suivant illustre une configuration standard.</span><span class="sxs-lookup"><span data-stu-id="73f0f-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="73f0f-163">Créer le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="73f0f-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="73f0f-164">Modifiez hello fichier tooadd hello nouvelle configuration SSH :</span><span class="sxs-lookup"><span data-stu-id="73f0f-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="73f0f-165">Exemple de fichier `~/.ssh/config` :</span><span class="sxs-lookup"><span data-stu-id="73f0f-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="73f0f-166">Ainsi la configuration SSH vous sections pour chaque serveur tooenable chaque toohave sa propre paire de clés dédié.</span><span class="sxs-lookup"><span data-stu-id="73f0f-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="73f0f-167">Hello des paramètres par défaut (`Host *`) sont pour tous les hôtes qui ne correspondent pas à des hôtes spécifiques et hello plus haut dans le fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="73f0f-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="73f0f-168">Explication du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="73f0f-168">Config file explained</span></span>

<span data-ttu-id="73f0f-169">`Host`= nom hello d’hôte hello soit appelée sur hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="73f0f-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="73f0f-170">`ssh fedora22`Indique à `SSH` toouse les valeurs hello dans le bloc de paramètres hello étiqueté `Host fedora22` Remarque : hôte peut être toute étiquette logiques pour votre utilisation et ne représente pas un nom d’hôte réel de hello de n’importe quel serveur.</span><span class="sxs-lookup"><span data-stu-id="73f0f-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="73f0f-171">`Hostname 102.160.203.241`= l’adresse IP de hello ou le nom DNS pour le serveur hello sollicité.</span><span class="sxs-lookup"><span data-stu-id="73f0f-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="73f0f-172">`User ahmet`= toouse de compte d’utilisateur distant hello lors de la connexion toohello server.</span><span class="sxs-lookup"><span data-stu-id="73f0f-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="73f0f-173">`PubKeyAuthentication yes`= Indique SSH vous voulez toouse un toolog clé SSH dans.</span><span class="sxs-lookup"><span data-stu-id="73f0f-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="73f0f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= la clé privée SSH hello et toouse de clé publique correspondante pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="73f0f-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="73f0f-175">Connexion SSH sous Linux sans mot de passe</span><span class="sxs-lookup"><span data-stu-id="73f0f-175">SSH into Linux without a password</span></span>

<span data-ttu-id="73f0f-176">Maintenant que vous avez une paire de clés SSH et un fichier de configuration SSH configuré, vous êtes en mesure de toolog dans tooyour Linux VM rapidement et en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="73f0f-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="73f0f-177">Hello première que connexion de serveur tooa à l’aide d’une invite de commandes hello clé SSH vous pour la phrase secrète de hello pour ce fichier de clé.</span><span class="sxs-lookup"><span data-stu-id="73f0f-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="73f0f-178">Explication des commandes</span><span class="sxs-lookup"><span data-stu-id="73f0f-178">Command explained</span></span>

<span data-ttu-id="73f0f-179">Lorsque `ssh fedora22` est exécutée SSH tout d’abord localise et charge les paramètres à partir de hello `Host fedora22` bloc, puis charge tous les hello restant des paramètres à partir de hello dernier bloc, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="73f0f-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73f0f-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73f0f-180">Next Steps</span></span>

<span data-ttu-id="73f0f-181">Ensuite des toocreate les machines virtuelles Azure Linux utilise hello nouveau la clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="73f0f-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="73f0f-182">Machines virtuelles Azure qui sont créés avec une clé publique SSH en tant que compte de connexion hello sont mieux sécurisées que les machines virtuelles créées avec la méthode de connexion hello par défaut, les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="73f0f-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="73f0f-183">Les machines virtuelles Azure créées à l’aide de clés SSH sont par défaut configurées avec les mots de passe désactivés, bloquant ainsi les tentatives de déchiffrement par force brute.</span><span class="sxs-lookup"><span data-stu-id="73f0f-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="73f0f-184">Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="73f0f-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="73f0f-185">Créer une VM Linux sécurisé à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="73f0f-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="73f0f-186">Créer une VM Linux sécurisé à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="73f0f-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
