---
title: "Procédure détaillée de création d’une paire de clés SSH pour les machines virtuelles Linux dans Azure | Microsoft Docs"
description: "Découvrez les étapes supplémentaires permettant de créer une paire de clés publique et privée SSH pour les machines virtuelles Linux dans Azure, ainsi que des certificats spécifiques pour différents scénarios."
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="89c23-103">Procédure détaillée de création d’une paire de clés SSH et de certificats supplémentaires pour une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="89c23-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="89c23-104">Avec une paire de clés SSH, vous pouvez créer des machines virtuelles sur Azure qui utilisent par défaut des clés SSH pour l’authentification, éliminant ainsi la nécessité de recourir aux mots de passe pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="89c23-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="89c23-105">Les mots de passe sont vulnérables et peuvent exposer vos machines virtuelles à de constantes attaques par force brute visant à découvrir ces mots de passe.</span><span class="sxs-lookup"><span data-stu-id="89c23-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="89c23-106">Les machines virtuelles créées avec l’interface de ligne de commande Azure ou avec des modèles Resource Manager peuvent inclure votre clé publique SSH dans le cadre du déploiement, ce qui évite l’étape de configuration post-déploiement consistant à désactiver les connexions par mot de passe pour SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="89c23-107">Cet article fournit des étapes détaillées et des exemples supplémentaires de génération de certificats destinés, par exemple, à être utilisés avec les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="89c23-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="89c23-108">Si vous souhaitez rapidement créer et utiliser une paire de clés SSH, consultez [Créer une paire de clés publique et privée SSH pour les machines virtuelles Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="89c23-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="89c23-109">Présentation des clés SSH</span><span class="sxs-lookup"><span data-stu-id="89c23-109">Understanding SSH keys</span></span>

<span data-ttu-id="89c23-110">L’utilisation de clés publiques et privées SSH constitue le moyen le plus simple pour vous connecter à vos serveurs Linux.</span><span class="sxs-lookup"><span data-stu-id="89c23-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="89c23-111">Le [chiffrement par clé publique](https://en.wikipedia.org/wiki/Public-key_cryptography) est un moyen bien plus sécurisé que les mots de passe pour vous connecter à votre machine virtuelle Linux ou BSD dans Azure. Les mots de passe sont beaucoup plus exposés aux attaques par force brute.</span><span class="sxs-lookup"><span data-stu-id="89c23-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="89c23-112">Votre clé publique peut être partagée avec n’importe qui, mais vous seul (ou votre infrastructure de sécurité locale) possédez votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="89c23-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="89c23-113">La clé privée SSH doit être protégée par un [mot de passe très sécurisé](https://www.xkcd.com/936/) (source : [xkcd.com](https://xkcd.com)).</span><span class="sxs-lookup"><span data-stu-id="89c23-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="89c23-114">Ce mot de passe permet simplement d’accéder au fichier de clé privée SSH et **n’est pas** le mot de passe du compte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89c23-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="89c23-115">Lorsque vous ajoutez un mot de passe à votre clé SSH, il chiffre celle-ci à l’aide d’une clé AES 128 bits, la rendant inutilisable sans le mot de passe qui permet de la déchiffrer.</span><span class="sxs-lookup"><span data-stu-id="89c23-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="89c23-116">Si un attaquant parvient à voler votre clé privée, et que celle-ci n’a pas de mot de passe, il peut l’utiliser pour se connecter aux serveurs contenant la clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="89c23-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="89c23-117">En revanche, si la clé privée est protégée par un mot de passe, cette dernière ne peut pas être utilisée par l’attaquant. Le mot de passe fournit ainsi une couche supplémentaire de sécurité pour votre infrastructure sur Azure.</span><span class="sxs-lookup"><span data-stu-id="89c23-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="89c23-118">Cet article crée une paire de fichiers de clés publique et privée SSH RSA de version de protocole 2 (également appelées clés « ssh-rsa »), qui sont recommandés pour les déploiements sur Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89c23-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="89c23-119">Les clés *ssh-rsa* sont nécessaires sur le [portail](https://portal.azure.com) pour les déploiements Classic et Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="89c23-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="89c23-120">Utilisation et avantages des clés SSH</span><span class="sxs-lookup"><span data-stu-id="89c23-120">SSH keys use and benefits</span></span>

<span data-ttu-id="89c23-121">Azure requiert au minimum des clés publique et privée SSH au format RSA de version de protocole 2 de 2 048 bits ; le fichier de clé publique possède le format de conteneur `.pub`.</span><span class="sxs-lookup"><span data-stu-id="89c23-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="89c23-122">Utilisez `ssh-keygen` pour créer les clés. Cette fonction pose une série de questions, puis génère une clé privée et une clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="89c23-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="89c23-123">Lors de la création d’une machine virtuelle Azure, Azure copie la clé publique dans le dossier `~/.ssh/authorized_keys` sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="89c23-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="89c23-124">Les clés SSH dans `~/.ssh/authorized_keys` servent à demander au client la clé privée correspondante sur une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="89c23-125">Lorsqu’une machine virtuelle Linux Azure est créée à l’aide de clés SSH pour l’authentification, Azure configure le serveur SSHD de façon à ne pas autoriser les connexions par mot de passe, mais uniquement les clés SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="89c23-126">Par conséquent, en créant des machines virtuelles Linux Azure avec des clés SSH, vous pouvez contribuer à sécuriser le déploiement de machines virtuelles et éviter l’étape de configuration classique après le déploiement qui consiste à désactiver les mots de passe dans le fichier **sshd_config**.</span><span class="sxs-lookup"><span data-stu-id="89c23-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="89c23-127">Utilisation de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="89c23-127">Using ssh-keygen</span></span>

<span data-ttu-id="89c23-128">Cette commande crée une paire de clés SSH (chiffrées) protégées par un mot de passe à l’aide du protocole RSA 2 048 bits. Elle fait l’objet d’un commentaire pour faciliter son identification.</span><span class="sxs-lookup"><span data-stu-id="89c23-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="89c23-129">Par défaut, les clés SSH sont conservées dans le `~/.ssh`répertoire.</span><span class="sxs-lookup"><span data-stu-id="89c23-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="89c23-130">Si vous n’avez pas de répertoire `~/.ssh`, la commande `ssh-keygen` en crée un pour vous avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="89c23-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="89c23-131">*Explication des commandes*</span><span class="sxs-lookup"><span data-stu-id="89c23-131">*Command explained*</span></span>

<span data-ttu-id="89c23-132">`ssh-keygen` = programme utilisé pour créer les clés</span><span class="sxs-lookup"><span data-stu-id="89c23-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="89c23-133">`-t rsa` = type de clé à créer correspondant au format RSA [wikipedia][parenthèses à la fin](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits de la clé</span><span class="sxs-lookup"><span data-stu-id="89c23-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="89c23-134">`-C "azureuser@myserver"` = commentaire ajouté à la fin du fichier de la clé publique pour l’identifier facilement.</span><span class="sxs-lookup"><span data-stu-id="89c23-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="89c23-135">Un courrier électronique est généralement utilisé comme commentaire, mais vous pouvez utiliser le contenu le mieux adapté à votre infrastructure.</span><span class="sxs-lookup"><span data-stu-id="89c23-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="89c23-136">Déploiement Classic à l’aide de `asm`</span><span class="sxs-lookup"><span data-stu-id="89c23-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="89c23-137">Si vous utilisez le modèle de déploiement Classic (mode `asm` dans l’interface de ligne de commande), vous pouvez utiliser une clé publique SSH-RSA ou une clé au format RFC4716 dans un conteneur .pem.</span><span class="sxs-lookup"><span data-stu-id="89c23-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="89c23-138">La clé publique SSH-RSA est l’élément créé précédemment dans cet article à l’aide de `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="89c23-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="89c23-139">Pour créer une clé au format RFC4716 à partir d’une clé publique SSH existante, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89c23-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="89c23-140">Exemple de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="89c23-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="89c23-141">Fichiers de clés enregistrés :</span><span class="sxs-lookup"><span data-stu-id="89c23-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="89c23-142">Nom de la paire de clés dans cet article.</span><span class="sxs-lookup"><span data-stu-id="89c23-142">The key pair name for this article.</span></span>  <span data-ttu-id="89c23-143">Le nom par défaut de la paire de clés est **id_rsa**. Certains outils pouvant demander le nom du fichier de clé privée **id_rsa**, il est utile d’en avoir un.</span><span class="sxs-lookup"><span data-stu-id="89c23-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="89c23-144">Le répertoire `~/.ssh/` est l’emplacement par défaut des paires de clés SSH et du fichier de configuration SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="89c23-145">Si aucun chemin d’accès complet n’est spécifié, `ssh-keygen` crée les clés dans le répertoire de travail actuel, et non dans le répertoire par défaut `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="89c23-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="89c23-146">Le contenu du répertoire `~/.ssh` s’affiche.</span><span class="sxs-lookup"><span data-stu-id="89c23-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="89c23-147">Mot de passe de clé :</span><span class="sxs-lookup"><span data-stu-id="89c23-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="89c23-148">`ssh-keygen` fait référence à un mot de passe utilisé pour la clé privée en tant que « phrase secrète ».</span><span class="sxs-lookup"><span data-stu-id="89c23-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="89c23-149">Il est *vivement* recommandé d’ajouter un mot de passe à votre clé privée.</span><span class="sxs-lookup"><span data-stu-id="89c23-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="89c23-150">Sans mot de passe pour protéger le fichier de clés, toute personne disposant du fichier peut l’utiliser pour se connecter à un serveur disposant de la clé publique correspondante.</span><span class="sxs-lookup"><span data-stu-id="89c23-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="89c23-151">L’ajout d’un mot de passe (phrase secrète) offre donc une meilleure protection, si un utilisateur malveillant a accès à votre fichier de clé privée. Vous avez ainsi plus de temps pour modifier les clés utilisées pour vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="89c23-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="89c23-152">Utilisation de ssh-agent pour stocker votre mot de passe de clé privée</span><span class="sxs-lookup"><span data-stu-id="89c23-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="89c23-153">Pour éviter de saisir le mot de passe de votre fichier de clé privée à chaque connexion SSH, vous pouvez utiliser `ssh-agent` pour le mettre en cache.</span><span class="sxs-lookup"><span data-stu-id="89c23-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="89c23-154">Si vous utilisez un Mac, le trousseau OSX stocke et sécurise les mots de passe de clés privées lorsque vous appelez `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="89c23-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="89c23-155">Vérifiez et utilisez ssh-agent et ssh-add pour indiquer au système SSH les fichiers de clés, afin qu’il ne soit pas nécessaire d’utiliser la phrase secrète de manière interactive.</span><span class="sxs-lookup"><span data-stu-id="89c23-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="89c23-156">Ensuite, ajoutez la clé privée à `ssh-agent` à l’aide de la commande `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="89c23-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="89c23-157">Le mot de passe de la clé privée est maintenant stocké dans `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="89c23-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="89c23-158">Copier la clé dans une machine virtuelle existante à l’aide de `ssh-copy-id`</span><span class="sxs-lookup"><span data-stu-id="89c23-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="89c23-159">Si vous avez déjà créé une machine virtuelle, vous pouvez installer la nouvelle clé publique SSH sur votre machine virtuelle Linux avec :</span><span class="sxs-lookup"><span data-stu-id="89c23-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="89c23-160">Créer et configurer un fichier de configuration SSH</span><span class="sxs-lookup"><span data-stu-id="89c23-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="89c23-161">Il est recommandé de créer et de configurer un fichier `~/.ssh/config` pour accélérer les connexions et optimiser le comportement de votre client SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="89c23-162">L’exemple suivant illustre une configuration standard.</span><span class="sxs-lookup"><span data-stu-id="89c23-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="89c23-163">Créer le fichier</span><span class="sxs-lookup"><span data-stu-id="89c23-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="89c23-164">Modifiez le fichier pour ajouter la nouvelle configuration SSH :</span><span class="sxs-lookup"><span data-stu-id="89c23-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="89c23-165">Exemple de fichier `~/.ssh/config` :</span><span class="sxs-lookup"><span data-stu-id="89c23-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="89c23-166">Cette configuration SSH propose des sections pour chaque serveur, permettant à chacun d’eux d’avoir sa propre paire de clés dédiée.</span><span class="sxs-lookup"><span data-stu-id="89c23-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="89c23-167">Les paramètres par défaut (`Host *`) sont destinés à tous les hôtes qui ne correspondent pas à ceux répertoriés plus haut dans le fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="89c23-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="89c23-168">Explication du fichier de configuration</span><span class="sxs-lookup"><span data-stu-id="89c23-168">Config file explained</span></span>

<span data-ttu-id="89c23-169">`Host` = nom de l’hôte appelé sur le terminal.</span><span class="sxs-lookup"><span data-stu-id="89c23-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="89c23-170">`ssh fedora22` indique à `SSH` d’utiliser les valeurs dans le bloc de paramètres intitulé `Host fedora22`. REMARQUE : la valeur Host peut correspondre à une quelconque étiquette logique du point de vue de votre utilisation et ne représente pas le nom d’hôte réel d’un serveur.</span><span class="sxs-lookup"><span data-stu-id="89c23-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="89c23-171">`Hostname 102.160.203.241` = adresse IP ou nom DNS du serveur en cours d’accès.</span><span class="sxs-lookup"><span data-stu-id="89c23-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="89c23-172">`User ahmet` = compte d’utilisateur distant à utiliser lors de la connexion au serveur.</span><span class="sxs-lookup"><span data-stu-id="89c23-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="89c23-173">`PubKeyAuthentication yes` = indique à SSH que vous souhaitez utiliser une clé SSH pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="89c23-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="89c23-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = clé privée SSH et clé publique à utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="89c23-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="89c23-175">Connexion SSH sous Linux sans mot de passe</span><span class="sxs-lookup"><span data-stu-id="89c23-175">SSH into Linux without a password</span></span>

<span data-ttu-id="89c23-176">Maintenant que vous avez une paire de clés SSH et un fichier de configuration SSH configuré, vous pouvez vous connecter à votre machine virtuelle Linux rapidement et en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="89c23-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="89c23-177">Lors de votre première connexion à un serveur à l’aide d’une clé SSH, l’invite de commandes vous demande de saisir la phrase secrète du fichier de clé en question.</span><span class="sxs-lookup"><span data-stu-id="89c23-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="89c23-178">Explication des commandes</span><span class="sxs-lookup"><span data-stu-id="89c23-178">Command explained</span></span>

<span data-ttu-id="89c23-179">Lorsque `ssh fedora22` est exécuté, SSH commence par localiser et charger tous les paramètres du bloc `Host fedora22`, puis charge tous les paramètres restants du dernier bloc `Host *`.</span><span class="sxs-lookup"><span data-stu-id="89c23-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89c23-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89c23-180">Next Steps</span></span>

<span data-ttu-id="89c23-181">L’étape suivante consiste à créer des machines virtuelles Linux de Azure à l’aide de la nouvelle clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="89c23-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="89c23-182">Les machines virtuelles Azure créées avec une clé publique SSH comme identifiant de connexion sont mieux sécurisées que celles créées avec la méthode de connexion par défaut (les mots de passe).</span><span class="sxs-lookup"><span data-stu-id="89c23-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="89c23-183">Les machines virtuelles Azure créées à l’aide de clés SSH sont par défaut configurées avec les mots de passe désactivés, bloquant ainsi les tentatives de déchiffrement par force brute.</span><span class="sxs-lookup"><span data-stu-id="89c23-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="89c23-184">Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="89c23-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="89c23-185">Créer une machine virtuelle Linux à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="89c23-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="89c23-186">Créer une machine virtuelle Linux sécurisée à l’aide de l'interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="89c23-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
